# 知識種子庫

> 一頁紙筆記：快速查閱、立即套用的 AI Agent 開發知識

---

## 📚 知識清單

| 主題 | 適用場景 | 何時查閱 |
|------|---------|---------|
| [RAG 快速檢查單](rag-checklist.md) | 建立 RAG 系統 | 設計檢索增強生成功能時 |
| [Chain-of-Thought 範例](chain-of-thought.md) | 複雜推理任務 | 需要 AI 逐步思考時 |
| [Function Calling 最小示例](function-calling.md) | Agent 調用工具 | 讓 AI 執行實際動作時 |
| [Prompt 安全守則](prompt-security.md) | 防止注入攻擊 | 處理用戶輸入前 |
| [評估指標速查](evaluation-metrics.md) | 驗證 Agent 品質 | 建立測試與監控時 |

---

## 📖 使用方式

### 快速查閱
每篇筆記包含：
- **問題場景**：什麼時候用
- **最小代碼**：立即可用的範例
- **驗收點**：怎麼確認做對了
- **常見錯誤**：容易踩的坑

### 在 Copilot Chat 中引用
```
@workspace 參考 docs/knowledge/rag-checklist.md，幫我設計一個文件檢索系統
```

### 貢獻新筆記
1. 複製現有筆記的格式
2. 保持「一頁紙」原則（500 字以內）
3. 必須包含：場景、代碼、驗收、錯誤
4. 更新本 README 的清單

---

## 🔗 相關資源

- [Agent 產品化地圖](../Agent產品化地圖.md) — 策略與框架
- [Agent 評估標準](../agent評估標準.md) — Idea 評分表
- [Templates](../../templates/) — 可複用模板
