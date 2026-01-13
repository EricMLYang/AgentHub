# GitHub Copilot Instructions vs Claude.md

> 如何用指令檔客製化 AI 助手行為

---

## 核心概念

兩者都是「告訴 AI 如何協助這個專案」的設定檔：

- **GitHub Copilot**: `.github/copilot/instructions.md`
- **Claude Code**: `.claude/claude.md`

---

## 功能對比

| 功能 | GitHub Copilot | Claude Code |
|------|---------------|-------------|
| 檔案位置 | `.github/copilot/instructions.md` | `.claude/claude.md` |
| 支援工具 | VS Code (Copilot 擴充) | Claude Desktop/Web |
| 讀取方式 | 自動讀取為 workspace context | 自動讀取為 project context |
| 設定內容 | 角色定義、格式要求、禁止事項 | 角色定義、格式要求、禁止事項 |

---

## 為什麼需要 Instructions 檔？

### ✅ 好處

1. **一次設定，持續生效** — 不用每次都重複說明規範
2. **團隊共享** — 所有成員使用相同的 AI 協作標準
3. **專案特定** — 針對這個 repo 的特殊需求客製化
4. **品質一致** — 確保 AI 產出符合專案規範

### 📋 應該包含什麼？

- **角色定義**：AI 在這個專案的職責
- **產出格式**：需要什麼結構（如 Input/Output/Acceptance）
- **禁止事項**：避免空泛、大而化之、buzzword
- **工作流程**：與 prompts 的整合方式

---

## AgentHub 的實踐

我們的 `.github/copilot/instructions.md` 包含：

1. **明確角色** — Copilot 是協助「寫清楚想法」的夥伴
2. **格式要求** — 必須有 Input/Output/Acceptance
3. **驗收標準** — 可觀察、可否定、可測量
4. **禁止空泛** — 不要「提升效率」，要「省 10 分鐘」
5. **Prompts 整合** — 串接 idea → progress → result 工作流

---

## 延伸閱讀

- [GitHub Copilot Instructions 文件](https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
- [Claude Projects 文件](https://support.anthropic.com/en/articles/9517075-what-are-projects)

---

**日期**: 2026-01-13  
**標籤**: #vibe-coding #copilot #claude #ai-workflow
