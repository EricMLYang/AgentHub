# 評估指標速查

> 如何判斷你的 AI Agent「做得好不好」：從單次測試到持續監控

---

## 問題場景

**何時使用**：開發完成要上線前、需要比較不同版本、持續監控生產環境品質。

**不適合**：探索性 POC（先求有再求好）、創意生成任務（沒有標準答案）。

---

## 核心指標分類

### 1️⃣ 準確性指標（Accuracy Metrics）

| 指標 | 定義 | 計算方式 | 適用場景 |
|------|------|---------|---------|
| **Accuracy** | 正確率 | `正確數 / 總數` | 分類任務（情緒分析、意圖識別） |
| **Precision** | 精確率 | `TP / (TP + FP)` | 避免誤報（垃圾郵件偵測） |
| **Recall** | 召回率 | `TP / (TP + FN)` | 避免漏報（欺詐偵測、疾病篩檢） |
| **F1 Score** | 精確與召回的平衡 | `2 × (P × R) / (P + R)` | 同時在意誤報與漏報 |
| **BLEU** | 翻譯/生成品質 | n-gram 重疊度 | 翻譯、摘要生成 |
| **ROUGE** | 摘要品質 | 與參考答案的重疊 | 文本摘要 |

### 2️⃣ RAG 專用指標

| 指標 | 定義 | 評估內容 | 工具 |
|------|------|---------|------|
| **Context Precision** | 檢索精準度 | 檢索出的片段是否相關 | Ragas |
| **Context Recall** | 檢索召回率 | 是否檢索到所有必要資訊 | Ragas |
| **Faithfulness** | 忠實度 | AI 回答是否基於檢索內容（不編造） | Ragas |
| **Answer Relevancy** | 答案相關性 | 回答是否真的回答問題 | Ragas |

### 3️⃣ Agent 行為指標

| 指標 | 定義 | 觀察重點 |
|------|------|---------|
| **Task Success Rate** | 任務完成率 | 是否達成目標（下訂單、生成報告） |
| **Step Efficiency** | 步驟效率 | 完成任務用了幾步（越少越好） |
| **Tool Call Accuracy** | 工具調用準確度 | 是否調用正確的 Function |
| **Hallucination Rate** | 幻覺率 | 編造不存在資訊的頻率 |
| **Error Recovery** | 錯誤恢復能力 | 遇到 API 失敗是否能優雅降級 |

### 4️⃣ 成本與效能指標

| 指標 | 定義 | 目標 |
|------|------|------|
| **Latency (P50/P95)** | 回應時間 | P95 < 5 秒 |
| **Token Usage** | Token 消耗 | 控制成本 |
| **Cost per Task** | 單次任務成本 | < $0.10 |
| **Throughput** | 吞吐量 | 每秒處理請求數 |

---

## 最小代碼（快速評估）

### 1. 準備 Golden Set（測試集）
```python
golden_set = [
    {
        "input": "台北今天天氣如何？",
        "expected_tool": "get_weather",
        "expected_params": {"city": "台北"},
        "expected_answer_contains": ["晴天", "溫度"]
    },
    # ... 20-50 個測試案例
]
```

### 2. 自動化測試
```python
from ragas import evaluate
from ragas.metrics import faithfulness, answer_relevancy

results = []
for case in golden_set:
    response = agent.run(case["input"])
    results.append({
        "question": case["input"],
        "answer": response.answer,
        "contexts": response.retrieved_docs,
        "ground_truth": case["expected_answer"]
    })

# 用 Ragas 自動評分
scores = evaluate(results, metrics=[faithfulness, answer_relevancy])
print(scores)
```

### 3. 人工評估（小規模）
```python
# 隨機抽 10 個回答，人工打分
import random
sample = random.sample(results, 10)

for item in sample:
    print(f"問題：{item['question']}")
    print(f"回答：{item['answer']}")
    score = input("評分 (1-5): ")
    # 記錄到 CSV 或資料庫
```

---

## 驗收點

✅ **Golden Set 覆蓋率**：測試集涵蓋常見情境、邊界情況、錯誤輸入。  
✅ **自動化測試**：每次改動後自動跑測試，及早發現退化（Regression）。  
✅ **人工抽檢**：每週隨機抽 10-20 個生產環境回答，人工評分。  
✅ **成本監控**：每個任務平均花費 Token 數，確保不超預算。  
✅ **延遲監控**：P95 延遲 < 5 秒（否則影響用戶體驗）。  
✅ **錯誤率**：每天錯誤數 / 總請求數 < 5%。

---

## 常見錯誤

❌ **測試集太小**（< 10 個）：無法代表真實情況。  
❌ **測試集分佈偏差**：只測簡單情況，沒測邊界與錯誤輸入。  
❌ **只看整體分數**：沒分析哪些類型的問題容易出錯。  
❌ **沒持續更新測試集**：用戶提出新問題，但測試集沒跟上。  
❌ **過度擬合測試集**：為了提高分數，針對測試集調優（但生產環境表現差）。  
❌ **沒監控生產環境**：只在開發時測試，上線後不管。

---

## 實際案例

### 案例 1：客服 Agent 評估
```python
metrics = {
    "任務完成率": 0.87,  # 87% 的對話成功解決問題
    "平均輪次": 3.2,     # 平均 3.2 輪對話解決
    "轉人工率": 0.13,    # 13% 需要轉人工
    "用戶滿意度": 4.1,   # 5 分制，平均 4.1 分
    "成本": "$0.08/對話"
}
```

### 案例 2：SQL 生成 Agent 評估
```python
test_results = {
    "語法正確率": 0.95,       # 95% 生成的 SQL 可執行
    "邏輯正確率": 0.82,       # 82% 查詢結果符合預期
    "安全性": 1.0,            # 100% 沒有危險操作（DROP、DELETE）
    "平均生成時間": "2.3秒",
    "Token 消耗": "平均 800 tokens/query"
}
```

---

## 進階技巧

### 1. A/B Testing（比較不同版本）
```python
# 50% 流量用舊模型，50% 用新模型
if random.random() < 0.5:
    response = agent_v1.run(query)
else:
    response = agent_v2.run(query)

# 比較兩個版本的指標
compare_metrics(agent_v1, agent_v2)
```

### 2. LLM-as-a-Judge（用 AI 評估 AI）
```python
judge_prompt = f"""
請評估以下回答的品質（1-5分）：
問題：{question}
回答：{answer}
檢索到的文件：{contexts}

評分標準：
1. 是否基於文件內容（不編造）
2. 是否完整回答問題
3. 語言是否通順

評分：
"""

score = llm.generate(judge_prompt)
```

### 3. 持續監控（Databricks Lakehouse Monitoring）
```python
# 自動記錄每次請求
log_request({
    "timestamp": datetime.now(),
    "user_id": user_id,
    "question": question,
    "answer": answer,
    "latency": latency,
    "token_usage": token_usage,
    "tool_calls": tool_calls
})

# 每日生成報告
daily_report = analyze_logs(date="2026-01-14")
# - 成功率：87%
# - P95 延遲：4.2 秒
# - 異常高頻問題：「如何退款」（50 次）
```

---

## 評估流程建議

```
1. 開發階段：
   - 準備 Golden Set（20-50 個測試案例）
   - 每次改動後跑自動測試
   - 人工檢查 10 個範例

2. 上線前：
   - 擴充 Golden Set（100+ 案例）
   - Stress Test（壓力測試）
   - 安全測試（Prompt Injection）

3. 生產環境：
   - 記錄所有請求到資料庫
   - 每日監控關鍵指標（成功率、延遲、成本）
   - 每週人工抽檢 20 個回答
   - 每月更新 Golden Set（加入新問題）
```

---

## 相關資源

- [Ragas - RAG 評估框架](https://github.com/explodinggradients/ragas)
- [Databricks Agent Evaluation](https://docs.databricks.com/en/generative-ai/agent-evaluation/index.html)
- [MLflow LLM Evaluate](https://mlflow.org/docs/latest/llms/llm-evaluate/index.html)
