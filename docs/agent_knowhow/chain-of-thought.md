# Chain-of-Thought 範例

> 讓 AI 像人類一樣「逐步思考」，提升複雜推理準確度

---

## 問題場景

**何時使用**：任務需要多步推理（數學計算、邏輯判斷、複雜分析）、AI 直接回答容易出錯。

**不適合**：簡單查詢（「今天幾號」）、需要即時性（直接查 API 更快）、創意生成（不需要邏輯推理）。

---

## 最小代碼（Prompt 範例）

### ❌ 不好的 Prompt（直接問）
```
用戶問題：「一輛車每小時跑 60 公里，跑了 2.5 小時，中途休息 30 分鐘加油，請問總共跑了多遠？」

回答：180 公里（錯！AI 可能把休息時間也算進去）
```

### ✅ 好的 Prompt（Chain-of-Thought）
```
用戶問題：「一輛車每小時跑 60 公里，跑了 2.5 小時，中途休息 30 分鐘加油，請問總共跑了多遠？」

請一步步思考：
1. 列出已知條件
2. 識別關鍵變數
3. 逐步計算
4. 給出最終答案

回答：
1. 已知條件：速度 60 km/h，行駛時間 2.5 小時，休息 30 分鐘（0.5 小時）
2. 關鍵變數：距離 = 速度 × 實際行駛時間（休息不算）
3. 計算：60 km/h × 2.5 h = 150 公里
4. 最終答案：150 公里
```

---

## 進階技巧

### 1. Few-Shot CoT（給範例）
```python
prompt = """
範例 1：
問題：小明有 3 顆蘋果，小華給他 2 顆，他吃掉 1 顆，還剩幾顆？
思考：3 + 2 = 5，5 - 1 = 4
答案：4 顆

範例 2：
問題：一個班級有 30 人，60% 是女生，女生有幾人？
思考：30 × 0.6 = 18
答案：18 人

現在回答：
問題：{user_question}
思考：
"""
```

### 2. Zero-Shot CoT（簡單觸發）
```python
prompt = f"{user_question}\n\nLet's think step by step:"
```

### 3. Self-Consistency（多次推理取共識）
```python
# 用不同 temperature 生成 5 次推理
answers = []
for _ in range(5):
    answer = llm.generate(prompt, temperature=0.7)
    answers.append(answer)

# 取最常見的答案
final_answer = max(set(answers), key=answers.count)
```

---

## 驗收點

✅ **推理過程可追蹤**：AI 輸出包含「思考步驟」，不是只給最終答案。  
✅ **邏輯連貫性**：每一步推理合理，沒有跳躍或矛盾。  
✅ **答案正確性**：最終答案符合預期（準備 Golden Set 測試）。  
✅ **錯誤可診斷**：如果答錯，能從思考步驟看出哪一步出問題。  
✅ **成本可控**：Token 消耗增加約 2-3 倍，確認預算可接受。

---

## 常見錯誤

❌ **沒給「思考」的空間**：直接問「答案是什麼」，AI 容易亂猜。  
❌ **指令不明確**：只說「請思考」，AI 不知道要輸出推理過程。  
❌ **過度依賴 CoT**：簡單查詢也用 CoT，浪費 Token 和時間。  
❌ **沒驗證中間步驟**：只檢查最終答案，中間推理錯了也不知道。  
❌ **用在不需要邏輯的任務**：如「寫一首詩」、「生成廣告文案」。

---

## 實際案例

### 案例 1：數據異常診斷
```
今天銷售額比昨天低 50%，可能原因：
1. 檢查是否為假日（假日通常較低）
2. 檢查是否有系統故障（訂單是否有遺漏）
3. 檢查是否有促銷活動結束（昨天可能有活動）
4. 建議：先確認數據完整性，再分析業務原因
```

### 案例 2：SQL 查詢生成
```
需求：找出「過去 7 天內下單超過 3 次的用戶」
思考：
1. 時間範圍：CURRENT_DATE - INTERVAL '7 days'
2. 條件：COUNT(order_id) > 3
3. 分組：GROUP BY user_id
4. SQL：
SELECT user_id, COUNT(order_id) as order_count
FROM orders
WHERE order_date >= CURRENT_DATE - INTERVAL '7 days'
GROUP BY user_id
HAVING COUNT(order_id) > 3
```

---

## 相關資源

- [Chain-of-Thought Prompting 原始論文](https://arxiv.org/abs/2201.11903)
- [LangChain Self-Ask with Search](https://python.langchain.com/docs/modules/chains/popular/self_ask_search)
