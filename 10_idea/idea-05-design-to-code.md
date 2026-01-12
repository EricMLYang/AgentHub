# [Idea] Design-to-Code Agent

## 😫 痛點（現在多煩）

從設計稿到程式碼的過程耗時且容易出錯：
- 前端開發者需要手動解讀 Figma 設計
- 手動轉換成 React/Vue 元件
- 樣式、間距、顏色可能與設計不一致
- 需要反覆與設計師確認細節
- 缺少自動化工具，開發週期長

## 👤 目標使用者（誰會用）

- 前端開發者：需要將設計稿轉成程式碼
- 設計師：希望設計能快速落地
- 產品經理：希望加速開發流程

## 📥 輸入（Input）

- Figma Frame / Component（透過 Figma MCP 讀取）
- Design System / Design Tokens
- 元件庫規範
- 既有元件參考
- Figma API token

## 📤 輸出（Output）

- **React/Vue 元件程式碼**
  - 結構、樣式、基本互動
  - 符合 Design System
- **元件文件**（Markdown）
  - Props 說明
  - 使用範例
- **Pull Request**
  - 程式碼 + 文件
  - 設計預覽說明

## ✅ 驗收方式（Acceptance Criteria）

- [ ] 產生的元件通過 build 和 lint
- [ ] 產生的元件通過 unit test
- [ ] 樣式與設計稿一致（visual regression test）
- [ ] 使用的是 Design System 定義的 tokens 和元件
- [ ] spacing、字體大小、顏色等細節需設計師確認（HITL）
- [ ] Storybook + screenshot diff 測試通過
- [ ] 前端產出速度提升 40% 以上

## ⚠️ 風險/限制

- **設計規範缺口**：如果 Design System 不完整，生成品質會下降 → 先做「規範形式化（tokens/元件庫）」再談全自動
- 需要 Figma API 權限
- 複雜的互動邏輯仍需手動實作
- 設計稿與實際開發環境的差異（RWD、動態資料）

## 💭 其他補充

**Agent 化適配評分（1-5）**：
- 規則明確性：3（設計多樣、規範不齊會難）
- 可驗證性：4-5（build/test/lint + 視覺回歸）
- 回饋延遲：4（跑 UI preview、regression）
- 資料可得性：3-4（Design System 完整度決定一切）
- KPI：4（前端產出速度、改稿次數）
- 風險：2-3（品質與一致性）
- **總評：4/5（前提：Design System 夠形式化）**

**選型建議**：Workflow + Developer Agent
- 讀 Figma、產 code、開 PR 其實是「固定流程」，用 workflow 承接最穩；LLM 負責 mapping
- 真正 Agent 的價值在「遇到例外：缺 token、元件缺規範、樣式衝突」時能自主排障

**7 類型定位**：Developer Agent + Browser-using（讀 Figma）

**驗證閉環**：Storybook + screenshot diff / visual regression

相關工具參考：
- v0.dev（Vercel）
- builder.io
- Anima（Figma plugin）
