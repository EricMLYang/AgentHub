# GitHub Copilot 使用規範（AgentHub）

> 讓 Copilot 成為你的協作夥伴，而不是製造混亂的機器

---

## Copilot 在這個 Repo 的角色

GitHub Copilot 在 AgentHub 的任務是：

1. **協助寫清楚想法** — 把模糊的點子轉成具體的 Agent Idea（有 Input / Output / Acceptance）
2. **建立專案追蹤** — 從 idea 建立 InProgress 專案檔案，追蹤執行進度
3. **更新週報** — 把零散的筆記整理成結構化的週報，更新到專案檔案
4. **產出成功案例** — 完成專案後，整理成可複用的 Case Result
5. **定義驗收標準** — 把需求轉成可觀察、可否定的 Acceptance Criteria

---

## ✅ 產出格式要求

### 必須包含的內容
- **Input**：Agent 需要什麼資訊？
- **Output**：Agent 會產生什麼結果？
- **Acceptance**：怎麼確認 Agent 做對了？（可觀察、可否定）

### 驗收標準的好範例
✅ 「測試覆蓋率達到 80%」（可測量）  
✅ 「找出所有不符合 style guide 的地方」（可檢查）  
✅ 「誤報率低於 5%」（可量化）

### 驗收標準的壞範例
❌ 「做得好」（無法定義）  
❌ 「優化生產力」（無法測量）  
❌ 「提升使用者體驗」（太模糊）

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

在 `.github/copilot/prompts/` 資料夾中有預先準備好的 prompts：

### 📝 Idea 階段
- **refine_idea.md** — 把模糊想法轉成清楚的 Agent Idea
- **define_acceptance.md** — 把需求轉成可測量的驗收標準

### 🚀 執行階段
- **add_new_progress.md** — 從 idea 建立 InProgress 專案追蹤檔案
- **write_weekly_update.md** — 更新專案週報到 InProgress 檔案

### 🎉 完成階段
- **show_result.md** — 產出成功案例到 30_case_result/ 資料夾

### 使用方式
1. 根據你的階段選擇對應的 prompt
2. 複製 prompt 內容到 Copilot Chat
3. 填入你的資訊（專案名稱、負責人、筆記等）
4. 讓 Copilot 產出結構化的內容
5. 檢查並調整（不要照單全收！）
6. 儲存到對應的資料夾（10_idea / 20_inProgress / 30_case_result）

---  
✅ 從簡單筆記產生完整的專案文件  
✅ 整理週報並更新到專案追蹤檔案  
✅ 量化效益並產出成功案例

### Copilot 不適合做什麼
❌ 決定要不要做這個 Agent（人來決定）  
❌ 評估商業價值（人來評估）  
❌ 替代團隊討論（Copilot 只是輔助）  
❌ 替代人工審核與判斷（始終需要人的把關
✅ 提供範例或模板  
✅ 幫忙寫清楚 Input / Output / Acceptance  
✅ 建議可能的風險或限制

### Copilot 不適合做什麼
❌ 決定要不要做這個 Agent（人來決定）  
❌ 評估商業價值（人來評估）  
❌ 替代團隊討論（Copilot 只是輔助）

---

## 🔄 持續改進

這份 instructions 會隨著團隊使用經驗而調整。如果你發現：

- Copilot 產出的內容不符合期待
- 有更好的 prompt 寫法
- 需要新的使用規範

## 📂 工作流程建議

### 1️⃣ 有新想法時
使用 `refine_idea.md` → 產出到 `10_idea/`

### 2️⃣ 開始執行時
使用 `add_new_progress.md` → 產出到 `20_inProgress/`

### 3️⃣ 每週更新時
使用 `write_weekly_update.md` → 更新 `20_inProgress/` 中的專案檔案

### 4️⃣ 完成專案時
使用 `show_result.md` → 產出到 `30_case_result/`

---

請開一個 Issue 討論，讓這份文件持續改進！

---

👉 開始使用：[Copilot Prompts](prompts/)  
👉 回到：[貢獻指南](../../CONTRIBUTING.md)
