# [Idea] MI 轉資料自動化 Agent

## 😫 痛點（現在多煩）

每次處理上游提供的數據檔案都需要：
- 手動檢查檔案格式與欄位是否符合 schema
- 處理各種格式不一致的問題（CSV、Excel、JSON）
- 標準化後手動觸發 Databricks Job
- 失敗時需要人工看 log、定位問題、修復、重跑
- 缺乏完整的處理紀錄與 trace

整個流程耗時且容易出錯，影響數據時效性。

## 👤 目標使用者（誰會用）

- 數據工程師：負責數據接收與轉換
- 數據分析師：需要穩定及時的數據來源
- 業務團隊：提供原始數據檔案的合作夥伴

## 📥 輸入（Input）

- 上傳的數據檔案（CSV / Excel / JSON 等多種格式）
- 標準 schema 定義
- 歷史轉換紀錄與規則
- Databricks Job 設定
- 失敗時的 Job log

## 📤 輸出（Output）

- **標準化後檔案**（符合 schema）
- **完整處理紀錄**（Trace/Log）
- **MI Report**（處理狀態、數據品質報告）
- **失敗原因分析與修復建議**
- 自動重跑機制（可修復問題）
- 寫入 Database + 產出 MI 報表

## ✅ 驗收方式（Acceptance Criteria）

- [ ] 轉換前：schema/型態/必填檢核通過
- [ ] 轉換後：對帳檢核（筆數/總和/關鍵指標一致）
- [ ] Golden set regression 測試通過
- [ ] 失敗時能準確定位問題（欄位、行數、錯誤類型）
- [ ] 修復建議可執行且有效（自動或半自動修復）
- [ ] 高風險寫入採「staging→審核→promotion」流程（HITL）
- [ ] 處理時間比人工快 80% 以上
- [ ] 成功率 > 90%

## ⚠️ 風險/限制

- **資料被「錯轉但看起來合理」**：最危險的情況 → 一定要做對帳與 regression 測試
- 檔案格式多樣性可能超出預期
- 需要 Databricks API 權限
- 大型檔案處理可能超時
- schema 變更時需要重新配置

## 💭 其他補充

**Agent 化適配評分（1-5）**：
- 規則明確性：4（標準 schema/規範可形式化）
- 可驗證性：5（schema validator、對帳、row count、reconciler）
- 回饋延遲：4-5（跑 job 就知道）
- 資料可得性：5（歷史檔、轉換紀錄、job log）
- KPI：5（處理時間、成功率、重跑時間、人工 debug 時數）
- 風險：3-4（寫入 DB / 影響報表，需 guardrails）
- **總評：5/5（最值得投資的自用 Agent 主戰場）**

**選型建議**：Workflow（主）+ Code 驗證器（核心）+ Agent（除錯/診斷）
- 端到端流程很適合 Workflow：狀態清楚、分支有限、可治理
- 「檔案格式多樣」與「除錯定位」是 Agent 的甜蜜點：輸入變動大、需要推理與工具操作

**7 類型定位**：Business-task Agent（流程自動化）+ Analytics/Domain-specific（資料規範領域知識）

**驗證閉環**：
- 轉前：schema/型態/必填檢核
- 轉後：對帳（筆數/總和/關鍵指標）+ golden set regression
- HITL：高風險寫入採「staging→審核→promotion」
