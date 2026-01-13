# GitHub Copilot 使用規範（AgentHub）

> 讓 Copilot 成為你的協作夥伴，從想法到產品化的完整流程

---

## 🚀 快速開始

**本文件是 GitHub Copilot 在 AgentHub 的總指引。**

### 如何使用 Copilot 執行任務？

在 `.github/prompts/` 資料夾中，我們準備了完整的 prompt 模板：

- 🎨 **refine_idea.md** — 把模糊想法轉成結構化 Idea
- 📊 **evaluate-idea.md** — 評估 Idea 是否適合 Agent 產品化
- ✅ **define_acceptance.md** — 補充或優化驗收標準
- 🚀 **add_new_progress.md** — 建立專案追蹤檔案
- 📝 **write_weekly_update.md** — 更新專案週報
- 🎉 **show_result.md** — 產出成功案例

**使用方式**：
1. 打開對應的 prompt 檔案（例如 `refine_idea.md`）
2. 複製整個 prompt 內容
3. 在 GitHub Copilot Chat 中貼上
4. 根據 prompt 的指示填入你的內容
5. Copilot 會根據規範產出結構化結果

👉 詳細說明請見下方 [💡 如何使用 Prompts](#-如何使用-prompts) 章節

---

## Copilot 在這個 Repo 的角色

GitHub Copilot 在 AgentHub 的任務是：

1. **🎨 重寫想法（Refine）** — 把模糊的點子轉成結構化的 Agent Idea（痛點 / 使用者 / Input / Output / Acceptance）
2. **📊 評估想法（Evaluate）** — 用四階段框架評估 Idea 是否適合 Agent 產品化
3. **🚀 建立專案追蹤** — 從 idea 建立 InProgress 專案檔案，追蹤執行進度
4. **📝 更新週報** — 把零散的筆記整理成結構化的週報
5. **🎉 產出成功案例** — 完成專案後，整理成可複用的 Case Result

---

## ✅ Idea 格式要求

### 必須包含的欄位

1. **😫 痛點（現在多煩）**
   - 現在的做法有什麼問題？
   - 浪費多少時間？容易出什麼錯？
   - 必須具體、可量化

2. **👤 目標使用者（誰會用）**
   - 誰會用這個 Agent？
   - 他們的背景和需求是什麼？

3. **📥 輸入（Input）**
   - Agent 需要什麼資訊作為輸入？
   - 數據來源、檔案格式、API 等

4. **📤 輸出（Output）**
   - Agent 會產生什麼結果？
   - 交付形式、內容結構

5. **✅ 驗收方式（Acceptance Criteria）**
   - 怎麼確認 Agent 做對了？
   - 必須是可觀察、可否定、可測量的條件
   - 列出 3-7 條具體標準

6. **⚠️ 風險/限制**
   - 有什麼資料、權限、時間限制？
   - 可能會失敗的情況？
   - 需要人工介入（HITL）的環節？

### 驗收標準的好範例
git
✅ 「報告包含所有必要章節（概況、環比、細分、異常、洞察、來源）」（可檢查）  
✅ 「數值與來源數據一致（對帳檢核通過）」（可驗證）  
✅ 「測試覆蓋率達到 80%」（可測量）  
✅ 「找出所有不符合 style guide 的地方」（可檢查）  
✅ 「誤報率低於 5%」（可量化）  
✅ 「按時產出（準時率 > 95%）」（可追蹤）  
✅ 「產生的元件通過 build 和 lint」（可自動驗證）

### 驗收標準的壞範例

❌ 「做得好」（無法定義）  
❌ 「優化生產力」（無法測量）  
❌ 「提升使用者體驗」（太模糊）  
❌ 「報告品質優良」（主觀）  
❌ 「效能表現佳」（缺乏標準）

---

## 🚫 禁止事項

### 不要空泛
❌ 避免：「這個 Agent 可以幫助團隊提升效率」  
✅ 改成：「這個 Agent 可以讓每個 PR 省下 10 分鐘人工審查時間」

### 不要大而化之
❌ 避免：「建立一個全面的 AI 平台」  
✅ 改成：「建立一個可以自動審查 Python PR 的 Agent」

### 不要寫一堆 buzzword
❌ 避免：「leveraging cutting-edge LLM technology to revolutionize workflow automation」  
✅ 改成：「用 LLM 自動檢查 code style，省下人工審查時間」

---

## 💡 如何使用 Prompts

在 `.github/prompts/` 資料夾中有預先準備好的 prompts：

### 🎨 Idea 階段

#### **refine_idea.md** — 把模糊想法轉成結構化 Agent Idea
- **何時使用**：有一個想法但還不夠清楚時
- **產出**：包含痛點、使用者、Input/Output、驗收標準、風險的完整 Idea
- **產出位置**：`10_idea/`
- **使用方式**：
  1. 複製 refine_idea.md 中的 prompt
  2. 在 `[在這裡貼上你的想法]` 處填入你的原始想法
  3. Copilot 會產出結構化內容
  4. 檢查並調整（特別是驗收標準是否夠具體）
  5. 儲存到 `10_idea/idea-XX-name.md`

#### **evaluate-idea.md** — 評估 Idea 是否適合 Agent 產品化
- **何時使用**：Idea 寫好後，想評估是否值得投入資源
- **產出**：四階段評估報告（策略定位、任務選型、適配評分、架構可行性）
- **使用方式**：
  1. 複製 evaluate-idea.md 的完整內容到 Copilot Chat
  2. 貼上你的 Idea 描述
  3. Copilot 會逐一評分並給出總分與建議
  4. 根據評級（⭐⭐⭐強烈推薦 / ⭐⭐值得探索 / ⭐謹慎評估 / ❌不建議）決定下一步

#### **define_acceptance.md** — 補充或優化驗收標準
- **何時使用**：Idea 已有基本架構，但驗收標準不夠具體或缺失時
- **產出**：清晰、可測量的驗收標準列表
- **使用方式**：
  1. 複製 define_acceptance.md 的 prompt
  2. 貼上你的 Idea 或專案描述
  3. Copilot 會產出具體的驗收標準
  4. 檢查是否可觀察、可否定、可測量
  5. 更新到對應的 Idea 或 InProgress 檔案

### 🚀 執行階段

#### **add_new_progress.md** — 從 idea 建立 InProgress 專案追蹤檔案
- **何時使用**：決定要執行某個 Idea，需要建立專案追蹤
- **產出**：`20_inProgress/` 中的專案檔案
- **使用方式**：
  1. 複製 add_new_progress.md 的 prompt
  2. 提供 Idea 的檔案路徑或內容
  3. Copilot 會產生完整的 InProgress 專案檔案
  4. 確認內容後儲存到 `20_inProgress/`

#### **write_weekly_update.md** — 更新專案週報到 InProgress 檔案
- **何時使用**：每週更新專案進度時
- **產出**：更新後的 InProgress 檔案
- **使用方式**：
  1. 複製 write_weekly_update.md 的 prompt
  2. 提供本週的進度筆記或重點
  3. Copilot 會整理成結構化週報並更新檔案
  4. 檢查數據與日期是否正確

### 🎉 完成階段

#### **show_result.md** — 產出成功案例到 `30_case_result/` 資料夾
- **何時使用**：專案完成，需要整理成可複用的案例
- **產出**：`30_case_result/` 中的案例文件
- **使用方式**：
  1. 複製 show_result.md 的 prompt
  2. 提供 InProgress 檔案或專案總結
  3. Copilot 會產出包含效益量化的成功案例
  4. 確認數據準確性後儲存

---

## ✅ Copilot 適合做什麼

✅ 把零散想法轉成結構化 Idea  
✅ 評估 Idea 是否適合 Agent 產品化  
✅ 提供範例或模板（參考 10_idea/ 的案例）  
✅ 幫忙寫清楚 Input / Output / Acceptance  
✅ 建議可能的風險或限制  
✅ 從簡單筆記產生完整的專案文件  
✅ 整理週報並更新到專案追蹤檔案  
✅ 量化效益並產出成功案例  

### Copilot 不適合做什麼

❌ 決定要不要做這個 Agent（人來決定）  
❌ 評估商業價值（人來評估，Copilot 只提供框架）  
❌ 替代團隊討論（Copilot 只是輔助）  
❌ 替代人工審核與判斷（始終需要人的把關）  
❌ 保證 Idea 一定成功（評估只是參考）

---

## 📊 評估框架說明

使用 evaluate-idea.md 時，會經過四個階段：

### 第一階段：策略定位評估 (25%)
- Vertical AI 定位：是否針對特定行業？
- RaaS 轉型潛力：能否從「提供工具」進化為「交付成果」？
- 數據飛輪與護城河：能否透過使用累積數據？

### 第二階段：任務選型與技術路徑 (25%)
- 判斷是否真的需要 AI Agent（vs 純程式碼 / 工作流 / RAG）
- F.D.A 框架：Friction（摩擦點）、Data Nexus（數據交匯）、Actionable Outcome（可執行成果）

### 第三階段：Agent 化適配評分表 (40%)
- 規則明確性、結果可驗證性、回饋延遲性
- 重複性與頻率、狀態空間可模擬性、數據標註可得性

### 第四階段：架構可行性檢驗
- 數據基礎層、策略分析層、互動 Agent 層

**總分 8.0-10.0 = ⭐⭐⭐強烈推薦**  
**總分 6.0-7.9 = ⭐⭐值得探索**  
**總分 4.0-5.9 = ⭐謹慎評估**  
**總分 0-3.9 = ❌不建議**

---

## 🔄 持續改進

這份 instructions 會隨著團隊使用經驗而調整。如果你發現：

- Copilot 產出的內容不符合期待
- 有更好的 prompt 寫法
- 需要新的使用規範

請開一個 Issue 討論，讓這份文件持續改進！

---

## 📂 工作流程建議

### 1️⃣ 有新想法時
使用 `refine_idea.md` → 產出到 `10_idea/idea-XX-name.md`

**參考範例**：
- [idea-01-automated-analytics-reporting.md](../../10_idea/idea-01-automated-analytics-reporting.md) — 自動化數據分析報告
- [idea-05-design-to-code.md](../../10_idea/idea-05-design-to-code.md) — Design-to-Code Agent
- [idea-07-pm-agent.md](../../10_idea/idea-07-pm-agent.md) — PM Agent

### 2️⃣ 評估想法時
使用 `evaluate-idea.md` → 得到評分與建議

**檢查重點**：
- 總分是否 ≥ 6.0？
- 是否真的需要 Agent（vs 工作流/RAG）？
- 驗收標準是否可測量？
- 是否有數據飛輪機制？

### 3️⃣ 開始執行時
使用 `add_new_progress.md` → 產出到 `20_inProgress/`

### 4️⃣ 每週更新時
使用 `write_weekly_update.md` → 更新 `20_inProgress/` 中的專案檔案

### 5️⃣ 完成專案時
使用 `show_result.md` → 產出到 `30_case_result/`

---

👉 開始使用：[Copilot Prompts](prompts/)  
👉 回到：[貢獻指南](../../CONTRIBUTING.md)
