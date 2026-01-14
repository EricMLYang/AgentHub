# RAG 快速檢查單

> Retrieval-Augmented Generation：讓 AI 基於你的文件回答問題

---

## 問題場景

**何時使用**：AI 需要回答「你的專有知識」（內部文件、產品手冊、客服記錄）但這些資料沒在訓練集裡。

**不適合**：通用知識問答（直接用 LLM）、需要即時數據（用 API）、複雜多步推理（用 Agent）。

---

## 最小代碼（Python + LangChain）

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.vectorstores import FAISS
from langchain.embeddings import OpenAIEmbeddings
from langchain.chat_models import AzureChatOpenAI
from langchain.chains import RetrievalQA

# 1. 切片文件
splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = splitter.split_documents(documents)

# 2. 建立向量庫
embeddings = OpenAIEmbeddings()
vectorstore = FAISS.from_documents(chunks, embeddings)

# 3. 檢索 + 生成
llm = AzureChatOpenAI(model="gpt-4")
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=vectorstore.as_retriever(search_kwargs={"k": 3})
)

# 4. 問答
answer = qa_chain.run("如何申請退款？")
```

---

## 驗收點

✅ **檢索精準度**：手動問 10 個問題，檢索出的 Top-3 片段是否包含答案。  
✅ **回答正確性**：AI 生成的答案是否符合文件內容（不能編造）。  
✅ **引用溯源**：回答是否附上來源片段與文件位置。  
✅ **處理未知**：文件中沒有的問題，AI 能否誠實回答「文件中未提及」。  
✅ **多語言支援**（若需要）：中英文檢索是否都有效。

---

## 常見錯誤

❌ **Chunk 切太大**（> 1000 字）→ 檢索不精準，無關內容混入。  
❌ **Chunk 切太小**（< 200 字）→ 上下文不足，AI 理解錯誤。  
❌ **沒設 overlap**（chunk_overlap=0）→ 關鍵句被切斷。  
❌ **Top-k 設太小**（k=1）→ 只檢索 1 個片段，容易遺漏資訊。  
❌ **Top-k 設太大**（k=10）→ 塞太多無關內容，干擾 AI 判斷。  
❌ **沒做 Rerank**：直接用 Embedding 距離排序，語意相關但不符合問題。  
❌ **沒過濾 Metadata**：檢索到過期文件、草稿或測試資料。

---

## 進階優化

1. **Hybrid Search**：結合關鍵字搜尋（BM25）+ 向量搜尋（Embedding）。
2. **Query Rewriting**：先讓 AI 改寫用戶問題，提升檢索效果。
3. **Reranking**：用 Cross-Encoder 對檢索結果重新排序。
4. **Metadata Filtering**：根據時間、部門、文件類型過濾。
5. **Self-Query**：讓 AI 自動決定要檢索哪個資料集。

---

## 相關資源

- [LangChain RAG 官方文件](https://python.langchain.com/docs/use_cases/question_answering/)
- [Databricks Vector Search](https://docs.databricks.com/en/generative-ai/vector-search.html)
