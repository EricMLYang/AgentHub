# [Idea] 設計 Review / QA Agent

## 😫 痛點（現在多煩）

設計品質檢查需要大量人工確認：
- 設計師需要手動檢查是否符合 Design System
- 確認 spacing、顏色、字體、元件使用是否正確
- 檢查多個 frame 耗時且容易遺漏
- 不一致的設計會增加開發成本與返工
- 缺少系統化的 QA 機制

## 👤 目標使用者（誰會用）

- 設計師：需要檢查自己或他人的設計稿
- Design Lead：需要確保團隊設計品質
- 前端開發者：希望設計稿符合規範，減少實作困難

## 📥 輸入（Input）

- Figma 設計稿（透過 Figma MCP 讀取）
- Design System 規範文件
- Design Tokens（顏色、間距、字體等）
- 元件庫定義
- Figma API token

## 📤 輸出（Output）

- **設計檢查報告**（PDF / Markdown / Web）
  - 不合規項目清單
  - 違規類型與嚴重程度
  - 修正建議
  - 截圖/位置標示
- 自動在 Figma 留言（標註問題位置）
- 通知設計師（Slack / Email）

## ✅ 驗收方式（Acceptance Criteria）

- [ ] 準確檢測出所有不符合 Design System 的項目
- [ ] 明確標示違規位置與類型
- [ ] 提供可執行的修正建議
- [ ] 支援例外白名單（允許特例）
- [ ] 設計師對「特例」做標註，回寫成規則/白名單（HITL）
- [ ] 檢查速度 < 30 秒（中型專案）
- [ ] 誤報率 < 5%
- [ ] 違規率下降 50% 以上

## ⚠️ 風險/限制

- **規範不完整或版本混亂**：如果 Design System 規範不明確，檢查會不準確 → 需要規範版本控管與套用範圍
- 需要 Figma API 權限
- 某些視覺品質（美感、可用性）無法自動檢查
- 特殊設計需求可能被誤判為違規（需要白名單機制）

## 💭 其他補充

**Agent 化適配評分（1-5）**：
- 規則明確性：5（Design System 就是規則）
- 可驗證性：5（比對 token/元件/spacing）
- 回饋延遲：5（即時）
- 資料可得性：4（規範文件+Figma data）
- KPI：4（違規率、返工次數）
- 風險：1-2（低風險）
- **總評：3/5（價值很高，但不需要「真正 Agent」）**

**選型建議**：Traditional code（規則檢查）+ Workflow（報告/通知）；LLM 可選
- 你要的多是「是否符合規範」：這是**規則引擎**工作，越少 LLM 越穩
- LLM 的角色可以是「把違規原因寫得更像人話」

**7 類型定位**：Business-task Agent（通知/流程）或偏「Lint 工具」

**驗證閉環**：規則引擎輸出 + 例外白名單（允許特例）

相關工具參考：
- Figma Linter plugins
- Design Lint
- Contrast (Figma plugin)
