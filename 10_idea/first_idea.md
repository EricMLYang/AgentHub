Team 數位化能力構想

---

## 一、數據與營運類 Agent

---

### 1️⃣ 自動化數據分析報告 Agent（Automated Analytics Reporting Agent）

**Agent 名稱**\
自動化數據分析報告 Agent

**實際產出成果（明確）**

- 結構化分析報告（Markdown / PDF / HTML）

   - 當期概況、環比/同比、細分貢獻、異常與風險、洞察與行動建議、需澄清事項、來源引用

- 排程產出（日/週/月）

- 發佈（Slack / Email / Confluence）

- 報告版本與審計紀錄

**實際動作**

- 讀 Databricks Gold Table/指標

- LLM 生成結構化敘事

- RAG：指標定義/PRD/儀表板說明 + 歷史報告（原子化）

- 排程、權限、稽核

**評論（選型＋Scorecard）**

- **選型建議：Workflow + RAG 為主；「部分 Agent」為輔**

   - 報告產出流程本身是**固定步驟**（取數→算指標→產出），用 **Workflow** 最穩。

   - LLM 的價值在**敘事一致性與可讀性**，用 **RAG** 讓用語與定義一致。

   - 真正 Agent 只放在「異常診斷/追因」等需要多步推理的段落。

- **Agent 化適配（1–5）**：

   - 規則明確性 **4**（章節固定、格式可規範）

   - 可驗證性 **4**（可用一致性檢查、引用完整性、數值對齊檢核）

   - 回饋延遲 **2–3**（洞察好壞常要人評，但格式/數值可秒級驗）

   - 資料可得性 **5**（數據、歷史報告、指標定義都存在）

   - KPI 清楚 **5**（準時率、錯誤率、人工省時）

   - 風險 **2**（錯誤可控、可加審核）

   - **總評：4/5（高 ROI，但不必全 Agent）**

- **7 類型定位**：Analytics Agent（主）+ Business-task Agent（排程/發佈）

- **驗證閉環**：

   - 自動驗證器：數值一致性、章節完整性、引用必填、異常閾值告警

   - **HITL**：洞察與行動建議先「草稿→審核→發佈」

- **風險點**：敘事幻覺、來源引用不嚴謹 → 用 RAG + 引用強制規則 + 報告 diff。

---

### 2️⃣ 爬蟲維運 Agent（Web Scraping Maintenance Agent）

**Agent 名稱**\
爬蟲維運 Agent

**實際產出成果**

- 異常偵測告警（資料缺失/結構變動）

- CSS/DOM 變更報告

- 修正建議（Selector/XPath）

- 重構建議文件

**實際動作**

- 定期跑爬蟲 + 品質檢查

- 比對歷史 DOM/CSS

- 偵測 selector 失效

- 產出修正與重構建議

- 發送告警

**評論（選型＋Scorecard）**

- **選型建議：Traditional code + Workflow 為底；Agent 用於「修復建議生成」**

   - 偵測（缺失率、欄位空值、DOM hash 變動）是**規則型**：用 code 最可靠。

   - 真的難的是「網站改版後 selector 怎麼修」→ 這段才值得 Agent/LLM。

- **Agent 化適配（1–5）**：

   - 規則明確性 **3**（偵測清楚，修復不一定）

   - 可驗證性 **4**（修復後能否成功抓到資料＝立即驗證）

   - 回饋延遲 **5**（秒級抓一次就知道）

   - 資料可得性 **4**（DOM 差異、歷史 selector、log）

   - KPI **4**（修復時間、失敗次數、人工介入率）

   - 風險 **3**（錯抓資料風險，中等）

   - **總評：4/5（很像程式任務，閉環強，非常適合）**

- **7 類型定位**：Business-task Agent（監控告警）+ Developer Agent（產修復 patch）

- **驗證閉環**：

   - sandbox 抓取測試、golden pages、抽樣比對（內容分布/欄位 regex）

   - **HITL**：自動開 PR，但 merge 需人工 review

- **風險點**：默默抓錯（最危險）→ 必須有資料分布校驗、抽樣人工 spot-check、對帳機制。

---

### 3️⃣ MI 轉資料 Agent（MI-to-Data Automation Agent）

**Agent 名稱**\
MI 轉資料自動化 Agent

**實際產出成果**

- 標準化後檔案（符合 schema）

- 完整處理紀錄（Trace/Log）

- MI Report

- 失敗原因分析與修復建議

**實際動作**

- 接收上傳檔

- 欄位/格式檢核 → 標準化

- 觸發 Databricks Job

- 失敗：解析 log、定位、提出修復、可重跑

- 寫 DB + 出 MI

**評論（選型＋Scorecard）**

- **選型建議：Workflow（主）+ Code 驗證器（核心）+ Agent（除錯/診斷）**

   - 端到端流程很適合 Workflow：狀態清楚、分支有限、可治理。

   - 「檔案格式多樣」與「除錯定位」是 Agent 的甜蜜點：輸入變動大、需要推理與工具操作。

- **Agent 化適配（1–5）**：

   - 規則明確性 **4**（標準 schema/規範可形式化）

   - 可驗證性 **5**（schema validator、對帳、row count、reconciler）

   - 回饋延遲 **4–5**（跑 job 就知道）

   - 資料可得性 **5**（歷史檔、轉換紀錄、job log）

   - KPI **5**（處理時間、成功率、重跑時間、人工 debug 時數）

   - 風險 **3–4**（寫入 DB / 影響報表，需 guardrails）

   - **總評：5/5（最值得投資的自用 Agent 主戰場）**

- **7 類型定位**：Business-task Agent（流程自動化）+ Analytics/Domain-specific（資料規範領域知識）

- **驗證閉環**：

   - 轉前：schema/型態/必填檢核

   - 轉後：對帳（筆數/總和/關鍵指標）+ golden set regression

   - **HITL**：高風險寫入採「staging→審核→promotion」

- **風險點**：資料被「錯轉但看起來合理」→ 一定要做對帳與 regression。

---

## 二、個人生產力 / 工程加速類 Agent

---

### 4️⃣ 個人 AI Agent（Personal Workflow Agent）

**Agent 名稱**\
個人 AI Workflow Agent

**實際產出成果**

- Vue 元件（.vue）

- Swagger API 文件

- Backend Model 程式碼\
   \-（未來）CRUD、測試案例

**實際動作**

- 設計/規格 → Vue SFC

- 畫面需求 → API request/response + Swagger

- SQL schema → backend model + 命名型態建議

**評論（選型＋Scorecard）**

- **選型建議：Developer Agent（IDE/Repo）最合理；不要做成 Autonomous Agent**

   - 這類工作是「寫碼、跑測試、lint、開 PR」：環境可模擬、可驗證，**像程式開發一樣閉環強**。

   - 但它的輸入其實不需要無限自主規劃，重點是**工具整合**（repo、lint、test）。

- **Agent 化適配（1–5）**：

   - 規則明確性 **3–4**（規範可寫死，但需求會飄）

   - 可驗證性 **5**（lint/test/build）

   - 回饋延遲 **5**（秒級）

   - 資料可得性 **4**（既有元件/規範/PR history）

   - KPI **4**（開發時間、review 迴圈、缺陷率）

   - 風險 **2–3**（主要是品質，不是安全）

   - **總評：4/5（非常適合放在 repo/IDE 的 agent 工作流）**

- **7 類型定位**：Developer Agent

- **驗證閉環**：CI（lint+test+build）+ snapshot test（UI）

- **HITL**：PR 必走 review；Agent 只能提案與產 patch。

- **風險點**：生成碼與你們架構不一致 → 用「樣板 repo + 範例元件」當約束（formalization）。

---

## 三、設計到程式碼（Design → Code）類 Agent

---

### 5️⃣ 設計 → 程式碼 Agent（Design-to-Code Agent）

**Agent 名稱**\
Design-to-Code Agent

**實際產出成果**

- React/Vue 元件程式碼

- 文件（Markdown）

- Pull Request

- 設計預覽說明

**實際動作**

- Figma MCP 讀 Frame/Component

- 解析結構樣式互動 → JSON

- 生成程式碼 + 文件

- push branch + 開 PR

**評論（選型＋Scorecard）**

- **選型建議：Workflow + Developer Agent**

   - 讀 Figma、產 code、開 PR 其實是「固定流程」，用 workflow 承接最穩；LLM 負責 mapping。

   - 真正 Agent 的價值在「遇到例外：缺 token、元件缺規範、樣式衝突」時能自主排障。

- **Agent 化適配（1–5）**：

   - 規則明確性 **3**（設計多樣、規範不齊會難）

   - 可驗證性 **4–5**（build/test/lint + 視覺回歸）

   - 回饋延遲 **4**（跑 UI preview、regression）

   - 資料可得性 **3–4**（Design System 完整度決定一切）

   - KPI **4**（前端產出速度、改稿次數）

   - 風險 **2–3**（品質與一致性）

   - **總評：4/5（前提：Design System 夠形式化）**

- **7 類型定位**：Developer Agent + Browser-using（讀 Figma）

- **驗證閉環**：Storybook + screenshot diff / visual regression

- **HITL**：PR review + 設計師確認（尤其 spacing/字體）

- **風險點**：設計規範缺口 → 先做「規範形式化（tokens/元件庫）」再談全自動。

---

### 6️⃣ 設計 Review / QA Agent（Design QA Agent）

**Agent 名稱**\
設計 Review / QA Agent

**實際產出成果**

- 設計檢查報告（PDF/Markdown/Web）

- 不合規清單、修正建議

- 截圖/位置標示

**實際動作**

- 讀 Figma

- 比對 Design System

- 產 QA 報告並通知

**評論（選型＋Scorecard）**

- **選型建議：Traditional code（規則檢查）+ Workflow（報告/通知）；LLM 可選**

   - 你要的多是「是否符合規範」：這是**規則引擎**工作，越少 LLM 越穩。

   - LLM 的角色可以是「把違規原因寫得更像人話」。

- **Agent 化適配（1–5）**：

   - 規則明確性 **5**（Design System 就是規則）

   - 可驗證性 **5**（比對 token/元件/spacing）

   - 回饋延遲 **5**（即時）

   - 資料可得性 **4**（規範文件+Figma data）

   - KPI **4**（違規率、返工次數）

   - 風險 **1–2**（低風險）

   - **總評：3/5（價值很高，但不需要「真正 Agent」）**

- **7 類型定位**：Business-task Agent（通知/流程）或偏「Lint 工具」

- **驗證閉環**：規則引擎輸出 + 例外白名單（允許特例）

- **HITL**：設計師對「特例」做標註，回寫成規則/白名單（logic atomization）。

- **風險點**：規範不完整或版本混亂 → 需要規範版本控管與套用範圍。

---

## 四、產品與專案管理類 Agent

---

### 7️⃣ PM Agent（Product Management Agent）

**Agent 名稱**\
PM Agent

**實際產出成果**

- 需求書、PRD、SPEC、Roadmap、任務清單、估時

- Daily/Sprint Report

- Project Track & Risk Report

**實際動作**

- 解析需求輸入

- 產出結構化文件

- 拆任務、依賴、估時與風險

- 週期性追蹤報告

**評論（選型＋Scorecard）**

- **選型建議：RAG + Workflow 為主；不要一開始就 Autonomous Agent**

   - 文件生成屬於「可格式化」：RAG + 範本最有效。

   - 真正難的是「決策與協調」：這部分**可驗證性弱、回饋延遲長**，不適合全自動 Agent。

   - 但「週報彙整、風險追蹤、狀態同步」是 Business-task agent 的好場景。

- **Agent 化適配（1–5）**：

   - 規則明確性 **2–3**（很多是 judgement）

   - 可驗證性 **2**（PRD 好壞難自動驗）

   - 回饋延遲 **1–2**（要等 sprint 結果、stakeholder feedback）

   - 資料可得性 **3–4**（會議紀錄、issue、PR、roadmap）

   - KPI **3**（省時、同步效率、風險提早率）

   - 風險 **2–3**（錯誤主要是溝通成本）

   - **總評：2.5/5（很有用，但更像「助理＋模板系統」）**

- **7 類型定位**：Conversational（入口）+ Business-task（週報/追蹤）+ Research（整理引用）

- **驗證閉環**：文件格式校驗、引用完整性、與 issue/PR 對齊檢查（但內容品質仍需人判）

- **HITL**：PRD/估時/風險分級必須人工確認（Gateways）。

- **風險點**：「看起來很合理但不對」→ 強制引用來源（issue/PR/會議）與差異比對。

---

## 補一個你會用得到的「整體排序」結論（依你的標準）

- **最值得做真正 Agent（ROI 高 + 可驗證閉環強）**

   1. **MI 轉資料 Agent（5/5）**

   2. **爬蟲維運 Agent（4/5）**

- **高價值但建議 Workflow/RAG 主體、Agent 只做最難那段**\
   3) 自動化數據分析報告 Agent（4/5，但別全 Agent）\
   4) Design-to-Code Agent（4/5，前提是 Design System 形式化）

- **價值高，但不需要「真正 Autonomous Agent」**\
   5) 設計 QA Agent（3/5，偏 lint/規則引擎）\
   6) PM Agent（2.5/5，偏 RAG + 模板 + 週報流程）

如果你下一步要把這段放回你的「第五部分：規劃 Agent 功能」當案例，我也可以幫你把每個評論濃縮成「兩行可貼進文件」的版本。