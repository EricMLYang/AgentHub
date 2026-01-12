# [InProgress] 自動化數據分析報告 Agent

> 📌 關聯 Idea: [idea-01-automated-analytics-reporting](../10_idea/idea-01-automated-analytics-reporting.md)  
> 🚀 開始日期: 2026-01-08  
> 📊 目前狀態: `🟢 Building`

---

## 📋 執行計畫

### Phase 1: 研究與設計 ✅
- [x] 完成技術調研（工具/框架選擇）
  - 選用 LangChain + OpenAI GPT-4 for 洞察生成
  - Databricks SDK for 數據提取
- [x] 確認資料來源與存取權限
  - 已取得 Databricks Token
  - 確認可存取 gold table
- [x] 設計系統架構圖
  - Data Layer → Analysis Layer → Generation Layer → Distribution Layer
- [x] 定義 API / Interface
  - ReportGenerator.generate(metric_name, time_range)
  - ReportDistributor.send(report, channels)
- [x] 建立 POC（Proof of Concept）
  - 完成單一指標的報告生成 POC

### Phase 2: 核心功能開發 🔄
- [x] 實作核心邏輯
  - 數據提取模組
  - 環比/同比計算引擎
- [x] 整合資料來源
  - Databricks 連接已完成
  - 歷史報告儲存 (PostgreSQL)
- [ ] 錯誤處理機制
  - 資料缺失處理
  - API 重試機制
- [ ] 基本測試案例

### Phase 3: 整合與測試
- [ ] 整合現有系統/工作流
- [ ] 端到端測試
- [ ] 效能測試
- [ ] 使用者測試（UAT）

### Phase 4: 部署與監控
- [ ] 部署到測試環境
- [ ] 部署到正式環境
- [ ] 建立監控與告警
- [ ] 撰寫使用文件

---

## 📝 開發紀錄

### Week 2026-W02 (01/06 - 01/12)

**本週完成**
- 完成 Databricks 數據提取模組，支援自動 retry
- 實作環比/同比計算邏輯
- 建立 PostgreSQL schema 儲存歷史報告
- 完成單一指標報告生成測試

**遇到的問題**
- **問題**: Databricks 查詢偶爾 timeout (>30s)
- **解決方案**: 
  1. 加入 query result cache
  2. 實作 async 查詢機制
  3. 設定 timeout 為 60s + retry 3 次

**下週計畫**
- 完成錯誤處理機制（資料缺失、API 異常）
- 撰寫 unit tests (目標覆蓋率 80%)
- 開始整合 Slack 通知功能

**需要協助**
- [ ] 需要 BI 團隊協助確認異常閾值設定（環比變動 >20% 算異常？）
- [ ] 需要 Confluence API token 進行整合測試

### Week 2026-W01 (12/30 - 01/05)

**本週完成**
- 完成技術選型與架構設計
- 取得 Databricks 存取權限
- 建立專案 repo 與基礎架構
- 完成 POC：單一指標報告生成

**遇到的問題**
- **問題**: Databricks Python SDK 文件不完整
- **解決方案**: 參考官方範例 + 實驗測試，建立內部使用文件

**下週計畫**
- 開始核心功能開發
- 整合歷史報告儲存

---

## 🔧 技術決策紀錄

### 決策 1: 選擇 LangChain 作為 LLM 編排框架
- **日期**: 2026-01-03
- **背景**: 需要整合 LLM 生成洞察與行動建議，並處理 prompt template 管理
- **選項**: 
  - 選項 A (LangChain): 成熟生態系、豐富的 integrations、強大的 prompt 管理
  - 選項 B (直接用 OpenAI API): 簡單輕量、完全控制、較少依賴
  - 選項 C (LlamaIndex): 專注於文件檢索、較適合 RAG 場景
- **決定**: 選擇 LangChain，原因是：
  - 需要 chain 多個步驟（數據分析 → 洞察生成 → 格式化）
  - 有豐富的 output parser 支援結構化輸出
  - 未來可能需要整合更多工具（如 Vector DB）
- **後果**: 增加約 5 個依賴套件，但換來更好的可維護性

### 決策 2: 使用 PostgreSQL 儲存歷史報告而非檔案系統
- **日期**: 2026-01-06
- **背景**: 需要儲存原子化報告並支援快速查詢與比對
- **選項**: 
  - 選項 A (檔案系統 + S3): 簡單、容易備份
  - 選項 B (PostgreSQL): 結構化查詢、交易保證、關聯查詢
  - 選項 C (NoSQL): 靈活 schema、水平擴展
- **決定**: 選擇 PostgreSQL，原因是：
  - 報告結構相對固定
  - 需要複雜查詢（如：找出過去 4 週同指標報告）
  - 團隊已有 PostgreSQL 維運經驗
- **後果**: 需要設計 schema 與 migration 流程，但查詢效能更好

### 決策 3: 人工審核機制採用「先生成後審核」模式
- **日期**: 2026-01-10
- **背景**: 洞察與建議段落需要人工審核，但要平衡自動化與品質
- **選項**: 
  - 選項 A: 先人工審核再發送（完全人工檢查）
  - 選項 B: 先發送有免責聲明，事後抽查（完全自動）
  - 選項 C: 先生成草稿，Slack 通知審核，確認後自動發送（混合）
- **決定**: 選擇選項 C，原因是：
  - 保留自動化效益（非阻塞式）
  - 提供品質把關機制（Slack 審核通知）
  - 緊急情況可設定「信任模式」跳過審核
- **後果**: 需要實作審核工作流與通知機制，預計多 2 天開發時間

---

## 🧪 測試 & 驗證

### 功能測試清單
- [x] 測試案例 1: 正常數據輸入，產生完整報告
- [x] 測試案例 2: 環比同比計算正確性（對照 Excel 手算結果）
- [ ] 測試案例 3: 數據缺失時的處理（顯示警告訊息）
- [ ] 邊界測試: 極端數值（0、負數、超大數）處理
- [ ] 錯誤處理: Databricks 連線失敗、timeout、權限不足

### 效能指標
| 指標 | 目標 | 目前 | 狀態 |
|------|------|------|------|
| 單一報告生成時間 | < 30s | 22s | ✅ |
| Databricks 查詢時間 | < 10s | 8s (cached: 0.5s) | ✅ |
| 洞察生成準確度 | > 90% | 待測試 | ⏳ |
| 按時產出率 | > 95% | 待部署 | ⏳ |

### 驗收標準檢核
參考原始 idea 的驗收標準：
- [x] 報告包含所有必要章節（概況、環比、細分、異常、洞察、來源）
- [x] 數值與來源數據一致（對帳檢核通過）
- [x] 所有數據引用必須標註來源
- [ ] 異常超過閾值時會自動標記並說明
- [ ] 按時產出（準時率 > 95%）
- [ ] 洞察與行動建議段落需經人工審核（HITL）
- [ ] 可產生報告 diff，比對與上期差異

---

## 💡 學習與調整

### 與原始 Idea 的差異
| 項目 | 原始計畫 | 實際執行 | 原因 |
|------|----------|----------|------|
| 報告儲存 | 檔案系統（Markdown） | PostgreSQL + JSON | 需要結構化查詢與快速比對 |
| 人工審核機制 | 未明確定義 | Slack 通知 + 確認流程 | 平衡自動化與品質要求 |
| 發佈渠道 | 同步發送 | 優先 Slack，其他待後續迭代 | 先求 MVP 完成最高優先需求 |

### 新發現的問題
1. **Databricks 查詢不穩定**: 偶爾 timeout，需要 retry 機制與 cache
2. **洞察品質波動**: LLM 生成的洞察有時過於籠統，需要更精確的 prompt engineering
3. **異常閾值設定**: 不同指標的異常標準不同，需要可配置化

### 優化機會
1. **Query Cache**: 已實作，將常用查詢 cache 1 小時，效能提升 90%
2. **Batch Processing**: 未來可支援批次生成多個報告，降低總時間
3. **Template System**: 可讓使用者自訂報告模板（未來功能）

---

## 🔗 相關資源

### 文件連結
- [系統架構圖](https://miro.com/xxx)
- [Databricks SDK 文件](https://docs.databricks.com/dev-tools/python-sql-connector.html)
- [Prompt Templates](https://github.com/xxx/prompts/)

### Code Repository
- Repo: `https://github.com/company/analytics-report-agent`
- Branch: `feature/core-engine`
- PR: [#12 - 實作核心數據提取與分析](https://github.com/company/analytics-report-agent/pull/12)

### 參考資料
- [LangChain Output Parsers](https://python.langchain.com/docs/modules/model_io/output_parsers/): 結構化輸出處理
- [內部 BI 報告規範](https://confluence.company.com/bi-standards): 確保格式一致性
- [類似專案參考](https://github.com/similiar-project): 學習錯誤處理模式

---

## 📊 成本與效益追蹤

### 投入時間
| 階段 | 預估時間 | 實際時間 | 差異 |
|------|----------|----------|------|
| 研究設計 | 16h | 18h | +2h |
| 核心開發 | 40h | 28h (進行中) | - |
| 測試整合 | 16h | - | - |
| 部署文件 | 8h | - | - |
| **總計** | **80h** | **46h** | - |

**時間差異說明**:
- 研究階段多花 2h: Databricks SDK 文件不清楚，需要額外實驗

### 預期效益
- 節省時間: **15 小時/週**（每份報告從 3h 降到 15min）
- 減少錯誤: **80%**（自動對帳與來源標註）
- 提升一致性: **100%**（統一格式與計算邏輯）

---

## 🚧 風險與阻礙

### 目前阻礙
| 阻礙 | 影響 | 負責人 | 預計解決日 | 狀態 |
|------|------|--------|------------|------|
| 等待 Confluence API token | 阻擋 Confluence 整合測試 | @it-team | 2026-01-15 | 🔴 |
| 異常閾值標準未確認 | 影響異常檢測準確度 | @bi-team | 2026-01-14 | 🟡 |

### 已解決的阻礙
- ~~Databricks 權限申請~~: 已於 2026-01-04 取得 (申請 3 天)
- ~~PostgreSQL 環境建立~~: 已於 2026-01-05 完成 (IT 團隊協助)

---

## ✅ 完成檢核清單

完成後才能移到 `30_completed`：

- [ ] 所有驗收標準達成
- [ ] 測試覆蓋率 > 80%
- [ ] 程式碼經過 PR review
- [ ] 使用文件已完成
- [ ] 部署到正式環境
- [ ] 監控與告警已設定
- [ ] 完成 Post-mortem / 專案回顧
- [ ] 撰寫 Share Win 分享

---

## 📌 備註

### 下一步重點
1. 本週完成錯誤處理機制
2. 提高測試覆蓋率到 80%
3. 與 BI 團隊確認異常閾值標準

### 團隊回饋
- Data Team 對 POC 反應正面，期待正式版本
- 建議增加「資料品質檢查」功能（未來迭代）
