# GitHub Copilot 專案設定說明  
## .github/agents 與 copilot-instructions.md 的差異與使用方式

在 GitHub Copilot 新一代 Agent 機制中，主要有兩種「專案層級設定」可以影響 Copilot 的行為：

- `.github/agents/`：定義「不同角色的 Agent」
- `.github/copilot-instructions.md`：定義「整個專案共用的開發規範與背景」

兩者用途不同，但可以搭配使用。

---

## 一、.github/agents 是什麼？

`.github/agents/` 用來定義 **自訂 Agent（Custom Agents / Agent Profiles）**。  
每個檔案代表一個「角色化的 Copilot Agent」，例如：

- planner.agent.md（規劃型 Agent）
- implementer.agent.md（實作型 Agent）
- reviewer.agent.md（Code Review Agent）

### 主要用途
- 拆分不同工作角色（規劃 / 實作 / 重構 / Review）
- 為不同角色設定不同的：
  - 行為指引（prompts / instructions）
  - 工具權限（tools, MCP servers）
  - 使用時機（是否允許自動推斷使用）

### 特性
- Repo 等級可版本控管
- 可被 Copilot Agent Mode / CLI / Agents panel 選擇使用
- 適合用於「多步驟任務、自動化流程、分工型 Agent」

---

## 二、copilot-instructions.md 是什麼？

`.github/copilot-instructions.md` 是 **整個專案的共用 Copilot 指令檔（Repo-wide Custom Instructions）**。

它的內容通常包含：

- 專案架構說明
- Build / Test / Run 方式
- Coding style / 命名規則
- 安全或限制規則（哪些不能改、哪些要特別小心）

### 主要用途
- 讓 Copilot 在「所有請求中自動帶入專案背景」
- 不論你用哪個 Agent 或一般 Copilot Chat，都會套用

### 特性
- 全域生效（repo 內所有 Copilot 請求）
- 偏向「規範 / 背景 /制度」
- 適合放穩定、不常變動的專案共通知識

---

## 三、兩者差異快速比較

| 項目 | .github/agents | copilot-instructions.md |
|------|----------------|--------------------------|
| 定位 | 定義「不同角色的 Agent」 | 定義「整個專案的共用規範」 |
| 作用對象 | Copilot Agent（可選擇的角色） | 所有 Copilot 請求 |
| 是否可多個 | 可以（多個 agent profiles） | 通常一份 |
| 內容重點 | 行為、角色、工具、流程 | 架構、規範、背景、風格 |
| 使用時機 | 多角色分工 / 自動化流程 | 專案長期穩定規則 |

---

## 四、建議使用方式（最佳實務）

### 基本配置（建議必備）
- `.github/copilot-instructions.md`  
  → 放「專案共通規範與背景」

### 進階配置（Agent 化專案）
- `.github/agents/`  
  → 放「角色型 Agent」，例如：
  - Planner：只做需求拆解與計畫
  - Implementer：負責寫 code + 測試
  - Reviewer：只做 review，不直接改碼

### 概念對照
- copilot-instructions.md =「公司制度 / 專案規範」
- .github/agents =「不同職能員工的工作手冊 + 工具權限」

---

## 五、結論

- 如果你只想讓 Copilot「更懂這個專案」 → 用 `copilot-instructions.md`
- 如果你想建立「多角色 Agent 工作流」 → 一定要用 `.github/agents`
- 最強組合：  
  **copilot-instructions.md（穩定規範） + .github/agents（可擴充角色與流程）**

