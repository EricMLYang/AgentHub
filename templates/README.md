# AgentHub 模板庫

> 集中管理所有可複用的模板，讓 Copilot 與團隊成員輕鬆套用

---

## 📂 模板分類

### 1. Prompts 模板（`prompts/`）
用於 Copilot Chat 的結構化提示詞，幫助團隊快速產出高品質內容。

| 模板 | 用途 | 使用時機 |
|------|------|----------|
| [refine_idea.md](prompts/refine_idea.md) | 將模糊想法轉成結構化 Idea | 有新點子但還不清晰時 |
| [evaluate-idea.md](prompts/evaluate-idea.md) | 評估 Idea 是否適合 Agent 產品化 | Idea 成型後，決定是否投入資源 |
| [define_acceptance.md](prompts/define_acceptance.md) | 補充或優化驗收標準 | 驗收標準不夠具體時 |
| [add_new_progress.md](prompts/add_new_progress.md) | 從 idea 建立 InProgress 追蹤檔案 | 決定執行某個 Idea |
| [write_weekly_update.md](prompts/write_weekly_update.md) | 整理週報並更新專案檔案 | 每週更新進度時 |
| [show_result.md](prompts/show_result.md) | 產出成功案例到 case_result | 專案完成時 |

### 2. 重複任務模板（`repeat_task/`）
用於記錄團隊的重複性任務，作為 Agent 開發靈感來源。

- [template.md](repeat_task/template.md) — 重複任務記錄格式
- [ai-automation-guide.md](repeat_task/ai-automation-guide.md) — AI 化建議欄位說明與範例

### 3. 工作流程指令卡（`workflows/`）
用於指導 Copilot 執行多步驟流程。

- [idea-to-inprogress.md](workflows/idea-to-inprogress.md) — 將 Idea 轉換為 InProgress 專案追蹤檔案

### 4. 週報模板（`weekly/`）
（待補充：可從 00_weekly/ 提取標準格式）

---

## 🚀 如何使用模板

### 方法 1：在 Copilot Chat 中直接引用
```
@workspace 請套用 templates/prompts/refine_idea.md 模板，幫我整理以下想法：
[貼上你的想法]
```

### 方法 2：複製模板內容
1. 開啟對應的模板檔案
2. 複製完整內容到 Copilot Chat
3. 根據模板指示填入你的內容
4. Copilot 會根據格式產出結果

### 方法 3：檔案管理操作
- 新增重複任務：複製 `repeat_task/template.md` 到 `05_repeat_task.md/` 對應類別
- 建立週報：參考 `weekly/` 格式在 `00_weekly/` 新增檔案

---

## 📝 貢獻新模板

1. 在對應的子資料夾中新增 `.md` 檔案
2. 必須包含：
   - **用途說明**：這個模板解決什麼問題
   - **使用情境**：什麼時候該用
   - **填寫指引**：使用者需要提供什麼資訊
   - **範例**：至少一個完整範例
3. 更新本 README 的模板清單

---

## 🔗 相關資源

- [.github/copilot-instructions.md](../.github/copilot-instructions.md) — GitHub Copilot 使用規範
- [copilot-agent-plan.md](../copilot-agent-plan.md) — AgentHub 漸進式發展規劃
- [README.md](../README.md) — AgentHub 主文件
