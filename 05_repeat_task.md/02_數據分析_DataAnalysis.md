# 數據分析 (Data Analysis)

> 💡 關於「AI 化建議」欄位：請參考 [templates/repeat_task/ai-automation-guide.md](../templates/repeat_task/ai-automation-guide.md)

---

填寫人：@eric

描述：每週要手動把多個來源的曝光/觀看/停留指標整理成同一份表，還要補缺值與對齊欄位

同樣困擾：@alice @bob

時間成本：每次 45 分鐘；每週

**AI 化建議**：
- [ ] 數據提取與清洗 — 🟢 — Workflow — 省 15 分鐘
- [ ] 欄位對齊與缺值補充 — 🟢 — Workflow — 省 10 分鐘
- [ ] 異常值檢測 — 🟡 — Agent — 省 5 分鐘
- [ ] 數據驗證報告 — 🟢 — Workflow — 省 5 分鐘

---

填寫人：@eric

描述：自動化數據分析報告 Agent - 定期自動讀取 Databricks Gold Table/指標，用 LLM 生成結構化敘事報告（包含當期概況、環比/同比、細分貢獻、異常與風險、洞察與行動建議等），支援排程產出並發佈到 Slack/Email/Confluence

同樣困擾：

時間成本：原本需人工每週/月整理數據並撰寫報告，約 2-4 小時

**AI 化建議**：
- [x] 數據提取 — 🟢 — Workflow — 省 30 分鐘（已在 idea-01 實作中）
- [x] 環比/同比計算 — 🟢 — Workflow — 省 20 分鐘（已在 idea-01 實作中）
- [ ] 洞察敘事生成 — 🟡 — RAG + LLM — 省 60 分鐘（需人工審核）
- [ ] 異常診斷與追因 — 🟡 — Agent — 省 30 分鐘
- [ ] 多渠道發佈 — 🟢 — Workflow — 省 10 分鐘

**轉化狀態**：✅ 已轉為 [idea-01](../10_idea/idea-01-automated-analytics-reporting.md) 並進入開發

---

填寫人：

描述：

同樣困擾：

時間成本：
