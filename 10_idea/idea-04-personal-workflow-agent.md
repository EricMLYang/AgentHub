# [Idea] 個人 AI Workflow Agent

## 😫 痛點（現在多煩）

開發過程中有很多重複性高的工作：
- 根據設計/規格手寫 Vue 元件（結構相似但細節不同）
- 根據畫面需求手寫 API 文件（Swagger）與 request/response 格式
- 根據 SQL schema 手寫 backend model + 處理命名與型態對應
- 需要反覆調整、測試、修正
- 缺少自動化工具，增加開發時間

## 👤 目標使用者（誰會用）

- 前端開發者：需要快速產生 Vue 元件
- 後端開發者：需要產生 model 與 API 文件
- 全端開發者：需要端到端的開發加速

## 📥 輸入（Input）

- **Vue 元件**：設計稿 / 規格說明 / 既有元件參考
- **API 文件**：畫面需求 / 資料欄位說明 / 既有 API 參考
- **Backend Model**：SQL schema / table 定義 / 命名規範
- Repo 架構與規範文件
- 既有元件/API/Model 範例

## 📤 輸出（Output）

- **Vue 元件**（.vue 檔案）
  - 完整的 template + script + style
  - 符合專案規範
- **Swagger API 文件**
  - request/response 格式
  - 參數說明與驗證規則
- **Backend Model 程式碼**
  - 命名與型態對應
  - 基本 CRUD（未來）
  - 測試案例（未來）

## ✅ 驗收方式（Acceptance Criteria）

- [ ] 產生的程式碼通過 lint 檢查
- [ ] 產生的程式碼通過 unit test
- [ ] 產生的程式碼能成功 build
- [ ] UI 元件符合設計稿（snapshot test）
- [ ] 產生的程式碼符合專案架構規範
- [ ] 所有產出需經過 PR review（HITL）
- [ ] 開發時間減少 30% 以上
- [ ] Review 迴圈次數減少

## ⚠️ 風險/限制

- **生成碼與架構不一致**：可能不符合專案規範 → 用「樣板 repo + 範例元件」當約束（formalization）
- 需要清楚的規範文件與範例
- 複雜的業務邏輯仍需人工處理
- 生成的程式碼品質依賴輸入的清晰度

## 💭 其他補充

**Agent 化適配評分（1-5）**：
- 規則明確性：3-4（規範可寫死，但需求會飄）
- 可驗證性：5（lint/test/build）
- 回饋延遲：5（秒級）
- 資料可得性：4（既有元件/規範/PR history）
- KPI：4（開發時間、review 迴圈、缺陷率）
- 風險：2-3（主要是品質，不是安全）
- **總評：4/5（非常適合放在 repo/IDE 的 agent 工作流）**

**選型建議**：Developer Agent（IDE/Repo）最合理；不要做成 Autonomous Agent
- 這類工作是「寫碼、跑測試、lint、開 PR」：環境可模擬、可驗證，像程式開發一樣閉環強
- 但它的輸入其實不需要無限自主規劃，重點是**工具整合**（repo、lint、test）

**7 類型定位**：Developer Agent

**驗證閉環**：CI（lint+test+build）+ snapshot test（UI）
