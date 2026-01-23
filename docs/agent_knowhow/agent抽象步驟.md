
An Illustrated Guide to AI Agents, Chapter 4. Planning and Reflection
---

## 重新對焦後的評估

讀完原文後，我需要修正一些先前的判斷。這份教材的核心價值和侷限現在更清晰了。

---

## 原文真正在講什麼

這份教材的脈絡是：

1. **Task Decomposition** → 把大問題拆成小問題
2. **Action Sequencing** → 決定執行順序，核心是 ReAct
3. **Reflection & Self-Improvement** → 從 Self-Refine、Reflexion 到 TTRL/R-Zero

關鍵洞察：原文明確區分了三個層次的技術實現方式：
- **Prompting**（ReAct、Self-Refine、Reflexion）
- **Supervised Fine-Tuning**（FireAct）
- **Reinforcement Learning**（ETO、TTRL、R-Zero）

---

## 對 Data Analysis Agent 的適用性重新評估

### ReAct 作為核心框架：適合，但要理解它的定位

原文對 ReAct 的定位很清楚：

> "ReAct decouples reasoning and planning... this framework interleaves both reasoning traces and task-specific actions to create an iterative process of thinking and taking actions."

ReAct 的 Thought-Action-Observation 循環對數據分析的價值在於：

| ReAct 元素 | 數據分析的對應 | 實際效果 |
|-----------|---------------|---------|
| **Thought** | 決定下一步查什麼、為什麼 | 讓分析有邏輯脈絡，不是亂查 |
| **Action** | 執行 SQL/Python | 實際取得數據 |
| **Observation** | 看到查詢結果或錯誤訊息 | 決定是否需要修正或繼續深入 |

**但原文也明確指出 ReAct 的侷限**：

> "ReAct Agents can theoretically go on for hundreds of cycles, but need to remember their previous steps and outcomes to effectively continue when context becomes an issue."

這對數據分析很關鍵——當分析進行到第 10 步，Agent 可能已經忘了第 1 步查到什麼。

---

### Reflexion 比單純 ReAct 更適合數據分析

原文對 Reflexion 的描述解決了我先前提到的「分析品質評估」問題：

> "Reflexion uses three entities: Actor LLM (executes actions), Evaluator LLM (assesses quality), Self-Reflection LLM (generates nuanced feedback)"

這個三角色架構對數據分析的意義：

```
[Actor LLM] → 寫 SQL、跑分析
     ↓
[Evaluator LLM] → 「這個分析結果合理嗎？」「回答了原始問題嗎？」
     ↓
[Self-Reflection LLM] → 「結果不合理是因為沒考慮 X 因素，下一步應該...」
     ↓
[Actor LLM] → 根據反思調整分析
```

**這比單純的 ReAct 多了一層「分析品質」的把關**，而不只是「程式有沒有報錯」。

---

### Plan-and-Solve vs Least-to-Most：選擇要看分析類型

原文對這兩者的區分很重要：

**Plan-and-Solve**（零樣本，先規劃再執行）：
> "The LLM is asked to devise a plan first and then solve the problem step-by-step"

**Least-to-Most**（逐步解決，前一步的答案餵進下一步）：
> "The solution of each subproblem is fed back into the LLM when attempting to solve the next problem"

對數據分析而言：

| 分析類型 | 更適合的方法 | 原因 |
|---------|-------------|------|
| **確認式**（算本月營收、比較 YoY） | Plan-and-Solve | 步驟可預測，先規劃效率高 |
| **探索式**（找異常、挖洞察） | Least-to-Most | 下一步取決於上一步發現什麼 |

我先前說「Plan-and-Solve 對探索性分析過度僵化」，原文的 Least-to-Most 其實就是解法。

---

## 原文沒覆蓋、但數據分析必須補的

### 1. 數據品質的 Observation 解讀

原文的 Observation 主要是：
> "A reasoning step about the result of the action"

但數據分析的 Observation 需要更結構化：

```python
# 不只是「看到結果」，而是要檢查：
observation = {
    "execution_status": "success",  # 語法層
    "row_count": 1547,              # 完整性層
    "null_percentage": {"revenue": 0.02, "date": 0.0},  # 品質層
    "sanity_checks": {              # 業務邏輯層
        "revenue_positive": True,
        "date_range_valid": True,
        "total_matches_detail": False  # ← 這裡有問題
    }
}
```

### 2. 業務知識的注入點

原文提到：
> "Analyze the existing codebase/data"

但沒有說明如何讓 Agent 知道：
- `status = 1` 代表什麼
- 公司定義的「活躍用戶」口徑
- 某些時間段的數據有已知問題

這需要在 **Task Decomposition 之前** 加一個「Context Loading」步驟。

### 3. Evaluator 的評估標準

原文的 Evaluator：
> "An LLM that assesses the quality of the current trajectory"

但沒有說 Evaluator 根據什麼標準評估。對數據分析，你需要明確定義：

```python
evaluation_criteria = {
    "answers_original_question": bool,  # 有沒有回答到問題
    "data_completeness": float,         # 數據是否完整
    "logical_consistency": bool,        # 邏輯是否一致
    "business_reasonableness": bool,    # 結論是否符合業務常識
    "actionability": float              # 結論是否可執行
}
```

---

## 修正後的設計建議

基於原文，你的 Data Analysis Agent 架構應該是：

```
[1. Context Loading]
    ↓
[2. Task Decomposition] ← 用 Least-to-Most 或 Plan-and-Solve（視分析類型）
    ↓
[3. ReAct Loop]
    ├─ Thought: 決定下一步分析
    ├─ Action: 執行 SQL/Python
    └─ Observation: 結構化的結果檢查（不只是看數字）
    ↓
[4. Reflexion Layer]
    ├─ Evaluator: 根據明確標準評估分析品質
    └─ Self-Reflector: 總結問題、建議下一步
    ↓
[5. 迭代或輸出]
```

---

## 總結：這份教材是好的設計參考嗎？

| 面向 | 評估 | 說明 |
|------|------|------|
| **ReAct 作為核心** | ✅ 適合 | 提供了迭代、自我修正的基礎框架 |
| **Reflexion 三角色** | ✅ 很適合 | 解決了「分析品質評估」的問題 |
| **Task Decomposition** | ✅ 適合 | Least-to-Most 對探索式分析特別有用 |
| **Self-Improvement (TTRL/R-Zero)** | ⚠️ 進階選項 | 對 MVP 來說太重，但長期值得考慮 |
| **數據品質處理** | ❌ 需補充 | 原文沒覆蓋，你需要自己設計 |
| **業務知識注入** | ❌ 需補充 | 原文沒覆蓋，這是數據分析的核心挑戰 |

**結論**：這份教材是合適的設計參考，特別是 ReAct + Reflexion 的組合。但它是為通用 Agent 寫的，你需要針對數據分析的特性（數據品質、業務邏輯、探索性分析）做補充設計。