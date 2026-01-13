# Prompt: 建立成功案例 (Case Result)

## 目的
當專案完成或達到重要里程碑時，整理成可複用的成功案例，分享給團隊和社群。

---

## 使用方式

### 1. 準備你的資訊

整理以下資訊（可以是筆記、bullet points、或直接從 InProgress 檔案複製）：
- 原始痛點是什麼？
- 你的 Agent 做了什麼？
- 實際效益（數字、時間節省、錯誤減少）
- 使用的技術/工具
- 關鍵學習或挑戰
- 其他人可以怎麼用？

### 2. 複製以下 prompt 到 Copilot Chat

```
請幫我建立一份成功案例文件。

**專案名稱**: [Agent 名稱]
**負責人**: @[你的名字]
**完成日期**: [YYYY-MM-DD]

請根據我的資訊，產生一份結構化的成功案例，包含：

1. **一句話總結**：這個 Agent 解決了什麼問題？
2. **背景與痛點**：原本的困擾是什麼？
3. **解決方案**：Agent 是如何運作的？
4. **實際效益**：量化的成果（時間、錯誤、效率）
5. **技術架構**：使用的工具與技術
6. **關鍵學習**：最重要的經驗是什麼？
7. **可複用性**：其他人可以如何使用或參考？

我的資訊：
[貼上你整理的資訊]
```

### 3. 檢查產出內容

確認清單：
- [ ] 有量化的效益數據？（時間、百分比、次數）
- [ ] 背景說明是否清楚？
- [ ] 解決方案是否具體可理解？
- [ ] 是否說明了可複用性？

### 4. 儲存到 30_case_result/

把內容儲存為：`30_case_result/case-[編號]-[簡短名稱].md`

命名範例：
- `case-01-auto-analytics-report.md`
- `case-02-vue-component-generator.md`

---

## 範例

### 輸入

```
請幫我建立一份成功案例文件。

**專案名稱**: 自動化數據分析報告 Agent
**負責人**: @Eric
**完成日期**: 2026-02-15

我的資訊：
- 原本每週要花 15 小時手動產生 5 份數據報告
- 現在 Agent 自動從 Databricks 提取數據、計算環比同比、生成洞察
- 每份報告從 3 小時降到 15 分鐘（包含人工審核）
- 使用 LangChain + OpenAI GPT-4 + Databricks SDK
- 關鍵挑戰是處理 Databricks timeout，用 cache + retry 解決
- BI 團隊和產品團隊都可以用來自動化週報
- 已部署到 Slack，每週一自動產出
```

### Copilot 產出

檔案：`30_case_result/case-01-auto-analytics-report.md`

````markdown
# [Case] 自動化數據分析報告 Agent

> 💡 **一句話總結**  
> 將手動數據分析報告流程自動化，每週節省 12.5 小時，錯誤率降低 80%

---

## 📌 基本資訊

- **負責人**: @Eric
- **完成日期**: 2026-02-15
- **相關專案**: [idea-01-automated-analytics-reporting](../10_idea/idea-01-automated-analytics-reporting.md)
- **狀態**: ✅ 已部署至正式環境

---

## 😫 背景與痛點

**原始情況**：
- 每週需要產出 5 份數據分析報告
- 每份報告需要 3 小時：手動從 Databricks 撈數據 → 計算指標 → 整理成結構化格式 → 發布到 Slack/Confluence
- 容易遺漏數據來源標註，造成後續追溯困難
- 不同分析師產出的報告格式不一致

**影響範圍**：
- BI 團隊 3 人每週共花費 15 小時
- 產品團隊等待報告時間長
- 重複性高，影響團隊士氣

---

## ✅ 解決方案

**Agent 運作流程**：

1. **自動數據提取**：每週一早上 9:00，從 Databricks Gold Table 提取指定指標
2. **智能分析**：
   - 自動計算環比/同比變化
   - 識別異常數據點（變動 >20%）
   - 分析細分維度貢獻度
3. **洞察生成**：使用 LLM 生成業務洞察與行動建議
4. **人工審核**：透過 Slack 通知相關人員審核洞察內容
5. **自動發布**：審核通過後，自動發送到指定 Slack 頻道

**關鍵特色**：
- 所有數據引用自動標註來源
- 支援多種報告模板
- 可配置異常閾值
- 完整的審計紀錄

---

## 📊 實際效益

### 量化成果

| 指標 | 之前 | 之後 | 改善 |
|------|------|------|------|
| 單份報告時間 | 3 小時 | 15 分鐘 | ⬇️ 92% |
| 每週總時間 | 15 小時 | 1.25 小時 | ⬇️ 92% |
| 資料錯誤率 | ~15% | ~3% | ⬇️ 80% |
| 報告一致性 | 低 | 高 | ✅ 100% |
| 按時產出率 | 85% | 98% | ⬆️ 15% |

### 實際節省
- **每週節省 12.5 小時**（3 人 × 4.17 小時/人）
- **每月節省約 50 小時** = 1.25 人月
- **年度節省約 600 小時** = 約 3.75 個月工作量

### 額外價值
- 團隊可將時間投入更深入的分析工作
- 報告品質更穩定，決策依據更可靠
- 新進人員無需學習報告產出流程

---

## 🔧 技術架構

### 核心技術棧
- **LLM 框架**: LangChain
- **AI Model**: OpenAI GPT-4
- **數據來源**: Databricks (Python SDK)
- **儲存**: PostgreSQL (歷史報告)
- **排程**: Airflow
- **通知**: Slack API
- **部署**: Docker + Kubernetes

### 系統架構
```
Airflow Scheduler
    ↓
Data Layer (Databricks SDK)
    ↓
Analysis Layer (計算引擎)
    ↓
Generation Layer (LangChain + GPT-4)
    ↓
Review Layer (Slack 通知)
    ↓
Distribution Layer (Slack API)
```

### 關鍵實作
- **Query Cache**: 常用查詢 cache 1 小時，效能提升 90%
- **Retry 機制**: 處理 Databricks timeout，3 次重試 + exponential backoff
- **Template System**: 可配置的報告模板，支援多種格式

---

## 💡 關鍵學習

### 1. LLM 輸出需要結構化
- **挑戰**: LLM 生成的洞察品質不穩定
- **解決**: 使用 LangChain Output Parser + few-shot examples
- **學習**: 好的 prompt engineering 是成功關鍵

### 2. 人機協作是最佳方案
- **挑戰**: 完全自動化 vs 完全人工，難以取捨
- **解決**: 先生成草稿 + Slack 審核機制
- **學習**: HITL (Human In The Loop) 平衡效率與品質

### 3. 錯誤處理比想像中重要
- **挑戰**: Databricks 查詢不穩定
- **解決**: Cache + Retry + Timeout 機制
- **學習**: Production 環境需要考慮更多邊界情況

### 4. 量化效益很重要
- **挑戰**: 一開始沒有記錄 baseline 數據
- **解決**: 後來補做時間追蹤與錯誤率統計
- **學習**: 從一開始就要設定可衡量的指標

---

## 🔄 可複用性

### 誰可以使用？
- ✅ **BI/數據團隊**：需要定期產出分析報告
- ✅ **產品團隊**：需要追蹤產品指標變化
- ✅ **業務團隊**：需要業務數據摘要
- ✅ **管理層**：需要快速了解關鍵指標

### 如何複用？

**直接使用**：
1. Fork 專案 repo
2. 配置你的 Databricks 連線
3. 定義你的指標與報告模板
4. 設定 Slack webhook
5. 啟動排程

**參考架構**：
- 數據來源可替換（BigQuery、Snowflake、MySQL）
- LLM 可替換（Claude、Gemini、開源模型）
- 通知渠道可替換（Email、Teams、Discord）

**核心可複用部分**：
- 環比/同比計算引擎
- LangChain prompt templates
- Retry 與 cache 機制
- 人工審核工作流

### 前置需求
- Databricks 或其他數據倉儲存取權限
- OpenAI API key 或其他 LLM API
- Slack workspace (或其他通知管道)
- 基本的 Python 與 Docker 知識

---

## 📎 相關連結

- **原始 Idea**: [idea-01-automated-analytics-reporting](../10_idea/idea-01-automated-analytics-reporting.md)
- **進度追蹤**: [20_inProgress/idea-01-automated-analytics-reporting](../20_inProgress/idea-01-automated-analytics-reporting.md)
- **Code Repo**: [github.com/company/analytics-report-agent](https://github.com/company/analytics-report-agent)
- **使用文件**: [Confluence - 數據報告 Agent 使用指南](https://confluence.company.com/agent-guide)

---

## 📝 更新紀錄

- **2026-02-15**: 完成初版，部署到正式環境
- **2026-02-20**: 新增支援 3 種報告模板
- **2026-03-01**: 優化 LLM prompt，洞察品質提升 25%

---

## 🎯 下一步

- [ ] 支援更多數據來源（BigQuery、Snowflake）
- [ ] 開發 Web UI 讓使用者自助配置報告
- [ ] 整合到 Confluence 自動更新文件
- [ ] 開源部分核心模組
````

---

## 小提示

**量化很重要**：盡量用數字說明效益（時間、百分比、次數）

**寫給別人看**：想像其他團隊成員讀這份文件，能否理解和複用？

**記錄學習**：不只寫成功的部分，也要記錄遇到的挑戰和解決方案

**更新可複用性**：說明清楚前置需求和複用步驟

**持續更新**：專案上線後的優化也要記錄

---

## 範本結構

完整的 Case Result 包含：
- 📌 基本資訊（負責人、日期、狀態）
- 😫 背景與痛點（原始問題）
- ✅ 解決方案（Agent 做什麼）
- 📊 實際效益（量化成果）
- 🔧 技術架構（工具與架構圖）
- 💡 關鍵學習（經驗與挑戰）
- 🔄 可複用性（誰能用、如何用）
- 📎 相關連結
- 📝 更新紀錄
- 🎯 下一步
