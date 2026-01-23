在 2026 年的 GitHub Copilot 生態系中，你所描述的「根據指令尋找並執行對應 Prompt」的機制已經非常成熟。這主要透過 **Prompt Files (# 選項)**、**Custom Instructions** 以及最新的 **Agent Mode 工具鏈** 來實現。

以下是此刻（2026 年）的最佳實務與操作指南：

---

## 核心機制：Prompt Orchestration (提示詞編排)

在 2026 年，最佳實務不再是寫一個超長的 System Prompt，而是將 Prompt **模組化**與**動態呼叫**。

### 1. Prompt Files (.github/prompts)

這是目前最推薦的標準作法。你可以將常用的「作業標準書 (SOP)」寫成 Markdown 檔案，存放在專案中。

* **路徑：** `.github/prompts/*.prompt.md`
* **用法：** 在 Copilot Chat 中輸入 `#prompt` 即可觸發。

### 2. executePrompt 工具 (Agent 專用，預覽版)

2026 年最新的 Copilot Agent Mode 具備了 **Tool Calling** 能力。其中最關鍵的工具就是 `executePrompt`。

* **機制：** 當你輸入「幫我重構這段程式碼」時，Agent 會檢查是否有對應的重構規範（如 `/refactor` 指令或 `refactor.prompt.md`），自動加載該 Prompt 的約束條件（如：必須符合 SOLID 原則、必須包含單元測試）。

---

## 2026 年的最佳實務流程

如果你想建立一個「自動化工作流」，通常會遵循以下結構：

### 步驟一：建立 Prompt 庫

在專案根目錄建立 `.github/prompts/`，例如建立一個 `security-check.prompt.md`：

```markdown
# 角色：資安專家
# 目標：審核選取的代碼是否存在常見漏洞 (OWASP Top 10)
# 格式：請以表格列出風險等級、描述與修復建議

```

### 步驟二：配置 Custom Instructions

在 `.github/copilot-instructions.md` 中告訴 Agent 如何尋找這些 Prompt：

> "Whenever the user asks for a review, always check `.github/prompts/` for relevant security or style guides before answering."

### 步驟三：指令觸發 (Slash Commands)

你可以自定義 **Slash Commands**。在 2026 年的環境中，這些指令可以直接映射到特定的 Prompt 文件：

* 輸入 `/api-gen` -> 自動觸發 `api-spec.prompt.md` 並讀取現有的 Swagger 文件。

---

## 實戰建議：如何「用」得更高效

| 功能 | 應用場景 | 2026 最佳實務 |
| --- | --- | --- |
| **動態上下文 (#)** | 需要針對特定檔案執行指令 | 使用 `#file` 或 `#codebase` 配合 `#prompt:security-check` |
| **Agent Skill** | 複雜的多步驟任務 (Plan -> Code -> Test) | 利用 **Agent Mode**，它會自動拆解任務並調用不同的子 Prompt |
| **MCP (Model Context Protocol)** | 需要讀取外部工具或專案管理系統時 | 透過 MCP 連接 Linear 或 Jira，讓 Agent 根據 Ticket 內容自動尋找 Prompt |

---

## 總結：此刻的開發範式

目前的趨勢是 **「解耦」**：

1. **指令 (Command)**：用戶輸入的自然語言。
2. **邏輯 (Prompt Template)**：存在 `.github/prompts` 中的結構化 Markdown。
3. **執行器 (Agent)**：GitHub Copilot Agent 負責匹配兩者，並透過 `executePrompt` 執行。

> **提示：** 確保你的 VS Code 設置中啟用了 `github.copilot.chat.executePrompt` 選項，這樣 Agent 才能擁有「調用其他 Prompt」的權限。

你想了解如何為特定的程式語言（如 Rust 或 TypeScript）建立一套自動化的 `.prompt.md` 範本嗎？