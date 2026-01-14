# Function Calling 最小示例

> 讓 AI 不只「說話」，還能「做事」：調用 API、查資料庫、執行程式碼

---

## 問題場景

**何時使用**：AI 需要取得即時資料（天氣、庫存、用戶資訊）、執行操作（發送郵件、建立工單、更新資料庫）。

**不適合**：純文字生成、不需要外部資料的任務、高風險操作（未經人工確認前）。

---

## 最小代碼（OpenAI Function Calling）

### 1. 定義 Function Schema
```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "取得指定城市的天氣資訊",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "城市名稱，例如：台北、東京"
                    },
                    "unit": {
                        "type": "string",
                        "enum": ["celsius", "fahrenheit"],
                        "description": "溫度單位"
                    }
                },
                "required": ["city"]
            }
        }
    }
]
```

### 2. AI 決定是否調用
```python
from openai import AzureOpenAI

client = AzureOpenAI(...)
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "台北今天天氣如何？"}],
    tools=tools,
    tool_choice="auto"  # AI 自動決定要不要調用
)

tool_call = response.choices[0].message.tool_calls[0]
print(tool_call.function.name)  # "get_weather"
print(tool_call.function.arguments)  # '{"city": "台北", "unit": "celsius"}'
```

### 3. 執行 Function 並回傳結果
```python
import json

# 解析參數
args = json.loads(tool_call.function.arguments)

# 執行實際函式
def get_weather(city, unit="celsius"):
    # 這裡應該調用真實的天氣 API
    return f"{city} 今天晴天，溫度 25°C"

result = get_weather(**args)

# 把結果回傳給 AI
response2 = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {"role": "user", "content": "台北今天天氣如何？"},
        response.choices[0].message,  # AI 的 tool call
        {"role": "tool", "tool_call_id": tool_call.id, "content": result}
    ]
)

print(response2.choices[0].message.content)
# "台北今天是晴天,溫度大約25度,適合外出活動。"
```

---

## 驗收點

✅ **Function 正確觸發**：用戶問「台北天氣」，AI 調用 `get_weather("台北")`，而不是胡亂猜測。  
✅ **參數正確解析**：AI 從自然語言中正確提取參數（城市、日期、數量等）。  
✅ **錯誤處理**：Function 執行失敗時，AI 能優雅降級（如：「目前無法取得天氣資訊」）。  
✅ **多步調用**：需要多個 Function 時（先查庫存、再下單），AI 能按順序執行。  
✅ **安全性**：敏感操作（刪除、付款）必須有人工確認（HITL）。

---

## 常見錯誤

❌ **Description 寫太模糊**：AI 不知道什麼時候該用這個 Function。  
  - 不好：`"處理用戶請求"`  
  - 好：`"當用戶詢問訂單狀態時，根據 order_id 查詢訂單資訊"`

❌ **沒定義 required 欄位**：AI 可能漏傳必要參數，導致 Function 執行失敗。

❌ **沒處理 Function 錯誤**：API 回傳 404，但沒告訴 AI，AI 繼續用錯誤結果回答。

❌ **無限循環**：AI 一直調用同一個 Function，沒有停止條件。

❌ **過度授權**：給 AI 太多危險權限（如：`delete_all_users`）。

---

## 進階技巧

### 1. 多 Function 協作
```python
tools = [
    {"type": "function", "function": {...}},  # check_inventory
    {"type": "function", "function": {...}},  # create_order
    {"type": "function", "function": {...}},  # send_confirmation_email
]

# AI 會自動決定調用順序：
# 1. check_inventory(product_id="A123")
# 2. create_order(user_id=1, product_id="A123")
# 3. send_confirmation_email(user_id=1, order_id=456)
```

### 2. 人工確認閘門（HITL）
```python
def sensitive_operation(**kwargs):
    # 危險操作必須人工確認
    print(f"⚠️ 即將執行：{kwargs}")
    confirm = input("確認執行？(y/n): ")
    if confirm.lower() != 'y':
        return "操作已取消"
    # 執行實際操作...
```

### 3. 結構化輸出
```python
# 強制 AI 回傳 JSON 格式（Databricks / OpenAI 都支援）
response = client.chat.completions.create(
    model="gpt-4",
    messages=[...],
    response_format={"type": "json_object"}
)
```

---

## 實際案例

### 案例 1：自動客服 Agent
```python
tools = [
    get_order_status,      # 查訂單
    cancel_order,          # 取消訂單（需人工確認）
    request_refund,        # 申請退款（需人工確認）
    search_faq,            # 搜尋 FAQ
]

user_query = "我要取消訂單 #12345"
# AI 自動調用：cancel_order(order_id="12345")
```

### 案例 2：數據分析 Agent
```python
tools = [
    execute_sql_query,     # 執行 SQL（唯讀）
    create_chart,          # 生成圖表
    send_report,           # 寄送報告
]

user_query = "過去 7 天銷售趨勢圖，寄給 PM"
# AI 自動：
# 1. execute_sql_query("SELECT date, SUM(amount) FROM sales WHERE ...")
# 2. create_chart(data, chart_type="line")
# 3. send_report(recipient="pm@company.com", attachment="chart.png")
```

---

## 安全建議

⚠️ **只開放必要權限**：不要給 AI `DROP TABLE` 權限。  
⚠️ **Dry Run 模式**：測試時用模擬數據，不要直接操作正式環境。  
⚠️ **操作日誌**：記錄所有 Function Call（誰、何時、做了什麼）。  
⚠️ **Rate Limiting**：防止 AI 無限調用同一個 API。  
⚠️ **Timeout**：設定 Function 執行時間上限，避免卡死。

---

## 相關資源

- [OpenAI Function Calling 官方文件](https://platform.openai.com/docs/guides/function-calling)
- [Databricks Agent Framework](https://docs.databricks.com/en/generative-ai/agent-framework/index.html)
- [LangChain Tools](https://python.langchain.com/docs/modules/agents/tools/)
