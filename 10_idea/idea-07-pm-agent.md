# [Idea] PM Agent

## 😫 痛點（現在多煩）

產品管理與專案追蹤工作繁瑣且重複：
- 需求整理與 PRD 撰寫耗時
- 任務拆解、估時、依賴關係複雜
- 需要定期產出 Daily/Sprint Report
- 專案狀態追蹤與風險辨識需要持續關注
- 多個工具之間的資訊同步（Jira / Confluence / Slack）
- 會議記錄整理與行動項追蹤

## 👤 目標使用者（誰會用）

- 產品經理：需要撰寫需求文件與追蹤專案
- 專案經理：需要掌握專案狀態與風險
- 開發團隊：需要清楚的需求與任務
- 管理層：需要了解專案進度與風險

## 📥 輸入（Input）

- 需求描述（文字 / 會議記錄）
- 專案資訊（Jira Issues / Pull Requests）
- 會議記錄與討論串
- 歷史 PRD / SPEC 文件
- Roadmap 與 Sprint 規劃
- 團隊資源與時程

## 📤 輸出（Output）

- **結構化需求文件**
  - PRD（Product Requirements Document）
  - SPEC（Technical Specification）
  - User Stories
- **專案規劃**
  - 任務清單（Task Breakdown）
  - 估時與依賴關係
  - Roadmap
- **追蹤報告**
  - Daily / Sprint Report
  - Project Status Report
  - Risk & Blocker Report

## ✅ 驗收方式（Acceptance Criteria）

- [ ] PRD 包含所有必要章節（目標、使用者、功能、驗收、風險）
- [ ] 文件格式符合團隊規範（模板檢查）
- [ ] 所有描述必須引用來源（issue/PR/會議記錄）
- [ ] 任務清單與 Jira issues 同步一致
- [ ] 估時與依賴關係需經團隊確認（HITL）
- [ ] 風險分級需人工確認（HITL）
- [ ] 週報產出準時率 > 95%
- [ ] 文件產出時間減少 40% 以上

## ⚠️ 風險/限制

- **「看起來很合理但不對」**：LLM 可能產生符合格式但內容不正確的文件 → 強制引用來源（issue/PR/會議）與差異比對
- **決策與協調難自動化**：涉及 judgement 的部分可驗證性弱、回饋延遲長，不適合全自動
- PRD/估時/風險分級必須人工確認
- 需要存取多個工具的 API（Jira / Confluence / Slack）

## 💭 其他補充

**Agent 化適配評分（1-5）**：
- 規則明確性：2-3（很多是 judgement）
- 可驗證性：2（PRD 好壞難自動驗）
- 回饋延遲：1-2（要等 sprint 結果、stakeholder feedback）
- 資料可得性：3-4（會議紀錄、issue、PR、roadmap）
- KPI：3（省時、同步效率、風險提早率）
- 風險：2-3（錯誤主要是溝通成本）
- **總評：2.5/5（很有用，但更像「助理＋模板系統」）**

**選型建議**：RAG + Workflow 為主；不要一開始就 Autonomous Agent
- 文件生成屬於「可格式化」：RAG + 範本最有效
- 真正難的是「決策與協調」：這部分可驗證性弱、回饋延遲長，不適合全自動 Agent
- 但「週報彙整、風險追蹤、狀態同步」是 Business-task agent 的好場景

**7 類型定位**：Conversational（入口）+ Business-task（週報/追蹤）+ Research（整理引用）

**驗證閉環**：
- 文件格式校驗
- 引用完整性檢查
- 與 issue/PR 對齊檢查
- 但內容品質仍需人判

相關工具參考：
- Linear（AI-powered project management）
- Notion AI
- Coda AI
