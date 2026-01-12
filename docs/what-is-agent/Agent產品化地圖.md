【 Databricks-first 團隊的 Agent 產品化自用地圖】

參考：Building Applications with AI Agents，簡立峰演講、ihower、海總理、Sean、曼報 Manny … 等各總 PO 文

地圖價值在於讓人知道，我在哪裡，可以往哪裡走。

我們團隊專注特定領域的 Databricks 數據中心 + 應用層系統，

預計明年會重壓 AI、Agent 功能，

因為是對外的產品想謹慎些，

所以個人列了一系列自我提問並用自製地圖來自我回答，

過程發現，

要全面的考量 AI 產品這件事，

要從 創投、產品經理、開發者視角來回跳動會比較全面，

以下是給自己參考的內容。

[ 第一部分: 為什麼要認真看待 Vertical AI]

[ 第二部分: 為你的 AI 產品定位]

[第三部分: AI Agent in Databricks]

[第部四分：領域現況與競爭態勢調研]

[第五部分: 規劃 Agent 功能]

[第六部分: 實現 Agent 的技術棧]

[第七部分: 實戰與案例]

▋自我拷問

我自己必須回答得出來的問題：

在 Databricks 數據中心 + 應用層 in 特定領域的架構，

如何挑出合理的 AI 功能與合適的生意模式，

並規劃出可行的技術框架

Q1. AI 時代，大環境怎麼變化?

．企業、外包、產品公司都用 AI 降本增效，合作邊界會怎麼變化？

．直接產生成果的服務，以及基於成果的收費是明確趨勢?

Q2. 目前 AI 產品大類?

．Vertical AI 本質是什麼? 和其他模式差異?

．Vertical AI 大類? 和各自商業模式是什麼?

Q3. AI 產品護城河是什麼?

．AI 產品的護城河體現在那些因素? 有飛輪效果嗎?

．產品能抵禦每次 LLM 能力提升後的取代性嗎?

Q4. 我們產品怎麼定位?

．原系統/Edge端 > Databricks 數據中心 > 應用層，其合適的 AI 產品以及各自角色?

．Databricks 是怎麼看待自家設計的 Agent 開發相關工具與服務?

Q5. 怎麼評估與比較不同的 Agent 功能?

．值得開發的 Agent 是什麼? 可系統性評估嗎?

．有什麼陷阱跟採坑重點嗎?

Q6. Agent 開發技術框架與團隊安排?

．開發 Agent 的必備技術棧?

．團隊怎麼分工?

[第一部分: 為什麼要認真看待 Vertical AI ]

本章拆解 AI 從「工具」轉向「成果交付」的演進，

剖析 Vertical AI 如何結合領域數據與工作流建立護城河，

助你評估商業價值與技術門檻。

給 LLM 研究的關鍵字： 

RaaS (成果導向收費)、Agentic Workflow、Data Flywheel、Model Distillation、Domain-specific RAG。

▋趨勢主流論述: 商業模式從 SaaS → WaaS → RaaS 的演進

1. Results as a Service (RaaS) - 成果導向收費

．原本按訂閱/席位收費，努力往按實際成果計費

．案例: 客服按「成功解決問題數」收費

．供應商與客戶利益深度綁定，形成「風險共擔」模式

2. Work as a Service (WaaS) - 工作量收費

．介於 SaaS 和 RaaS 之間的過渡模式

．按 AI 完成的工作量計費(如生成圖片數、處理文件數)

．現實常常會搭配訂閱/席位收費的混和模式

特點:

．端到端交付成果

．中國案例: 礦山自動駕駛企業從「賣軟體」轉為「承包運輸服務」

．Sierra (AI 客服): 按成功解決客戶問題收費，客戶滿意度達 70%

▋AI 時代下企業合作邊界變化

AI 讓能力不斷提高，

公司都想找會用 AI 的人來解決問題，

但 AI 同時也降低了，

原本業務外包公司的成本，

因此企業間合作邊界不斷的拉扯，

以下主要變化:

變化 1: 更重視 ROI 和成果

過去 IT 預算跟營收比起來很小，

主要考量工具成本，

現在 AI 功能的預算會影響營銷、業務預算，

ROI 和成果變成重要考量，

可能決策方向：

．高重複、可量化，有機會外包給 RaaS 供應商

．核心業務和專業，自建 + Vertical AI 發展

．探索性項目， 先 POC 再決定自建或外包

變化 2:外包公司被迫升級

傳統人力外派、按人頭收費模式，

在 AI 時代被取代性最高，

客戶期望的是更快、更便宜、更準確的成果，

轉型方向:

．Vertical AI 服務商: 深耕特定行業，提供端到端解決方案

．AI 人才培訓: 幫助企業團隊學會使用 AI 工具

．混合模式:「AI + 專家」協作，提供高附加價值服務

變化 3: 產品往 Vertical AI 走

Vertical 代表是針對特定行業跟場景，

AI 功能追求端到端成果，

Vertical AI 就是醫療 AI、法律 AI、金融分析 AI …等，

用 AI 去產出特定行業任務成果的產品，

商業模式:

．訂閱制 + 成果分潤

．平台化: 連接數據、模型、工具鏈

．生態系建設: 與雲端、數據平台深度整合

▋為什麼 Vertical AI 會是趨勢？

除了可直接展現成果說明 ROI 外，

是否容易被通用大模型取代也是重要一環，

通用產品的危險性在於，

通用模型能力太強，

模型 + 基本 RAG 就能做得不錯的事情，

當成產品題目就很危險。

用船跟海來比喻：

．通用模型海水每一次升級往上漲

．Vertical AI 要像船一樣，靠著獨特的利基優勢持續浮在海上

．而這多出來的成果，也是客戶認為有價值、願意買單的

如果覺得難以理解，可以思考：一

樣的優秀人才，在不同公司帶來的成果，

為什麼往往會差異很大。

▋AI 產品競爭優勢：技術實作維度

1. 特定 AI 能力：基於 System Prompt 的功能實現

這是競爭力最低的層次，

因為其核心邏輯僅存在於 Prompt (提示詞) 之中。

．技術本質：

開發者撰寫一段精良的 System Prompt，

定義角色（如：你是一個文案高手）並調用 LLM API。

．脆弱點：

對手只需透過 Prompt Injection 或簡單的逆向工程，

就能複製出相似的功能。

這類產品缺乏「狀態（State）」，

每一次調用都是獨立的。

2. 靜態資料：基於 RAG 的知識檢索

此層次的門檻在於「你餵了什麼資料給模型」，

通常透過 RAG (Retrieval-Augmented Generation) 實作。

．技術本質：

將非公開的產業文件進行 Chunking (切片)，

透過 Embedding Model 轉為向量存入 Vector Database。

當用戶提問時，

系統從資料庫檢索相關片段放入 Context Window 讓模型回答。

．脆弱點：資料本身是靜態的。

如果這些資料可以被購買或公開獲取，

對手只要建立相同的 Data Pipeline 並優化 Top-k Retrieval 的精準度，

就能消除你的優勢。

3. 領域 Know-how：基於邏輯注入與思維鏈 (CoT)

將專家的「解決問題流程」程式碼化或邏輯化。

．技術本質：

不只是檢索資料，

而是實作了 Few-shot Prompting（給予高質量的範例），

或 Chain-of-Thought (CoT) 提示技術。

你將專家的決策路徑拆解為多個步驟，

引導模型按照特定邏輯推理

（例如：先分析人流，再判斷天氣，最後生成廣告建議）。

．脆弱點：

這種邏輯雖然比單純的資料難複製，

但仍可被資深開發者觀察輸出結果後，

重新編寫邏輯模擬出來。

4. 過程數據：基於用戶反饋的微調 (Fine-tuning) 與對齊

這是護城河開始深化的轉折點，

數據不再是「買來的」，

而是「生出來的」。

．技術本質：

1.SFT (Supervised Fine-tuning)：

收集用戶修正 AI 建議後的「正確版本」，

作為標註數據對模型進行微調。

2.RLHF (Reinforcement Learning from Human Feedback) 的邏輯：

記錄用戶對建議的點擊（Accept）或拒絕（Reject），

建立 Preference Dataset。

．優勢：這讓模型學會了「該領域特有的偏好」。

對手即便有同樣的大模型，

也缺乏這份經過萬千用戶洗禮的 Fine-tuned Weights。

5. 深度整合 + 資料飛輪：

基於 Agent 與閉環管線 (Data Pipeline)

這是最高等級，

AI 已經從「對話框」進化為「執行者」。

．技術本質：

1.Function Calling / Tool Use：

AI 具備調用外部系統（如 POS 銷售數據、庫存 API）的能力。

．Agentic Workflow：

系統能自我迭代。

例如：AI 發布廣告後，自動獲取轉化率數據，

觸發 Automated Evaluation，

自動生成新一輪訓練數據進行 Incremental Learning。

．優勢：

對手不容易追趕，

因為你的模型是在一個「即時運行的生態系」中演化。

要複製你，

必須先複製客戶整套的硬體、系統整合與數年的運行數據。

▋Vertical AI 如何強化技術護城河？

Vertical AI 並非新技術，

而是將上述技術在特定場景「極端化」：

．完整工具鏈 (LLMOps 整合)：

Vertical AI 將 AI 嵌入在工作流中。

技術上，這代表你擁有完整的 Telemetry (遙測系統)，

能精準捕捉用戶在 UI 介面上的每一次滑鼠停頓與修改，

這些都是轉化為 Fine-tuning 的黃金數據。

．專有領域知識 (專用 Embedding & Tokenization)：

通用模型在處理特殊領域（如：電巴電池數據、半導體製程）時，

Tokenizer 可能效率極低，

或 Embedding 無法區分專業術語的微小差異。

Vertical AI 會針對領域開發 Domain-specific Embeddings，

讓 RAG 的檢索精準度達到商業等級的 99%，

而非通用的 80。

．內隱數據的自動化採集：

透過 Function Calling 串接業務系統，

AI 能看到「最終結果」（如：廣告真的賣出去了嗎？）。

這讓系統能自動生成 Ground Truth (地真數據)。

這種「自我標註」的能力，

是 Vertical AI 脫離人力依賴、實現規模化的關鍵。

．成本高度優化 (Model Distillation)：

利用 Model Distillation (模型蒸餾) 技術，

將 GPT-4 等大型模型的推理能力，

轉移到參數較小的模型（如 Llama-3-8B）。

Vertical AI 透過針對單一任務的 Full Parameter Fine-tuning，

讓小模型在特定領域表現優於大模型，

從而在 API 成本上建立經濟優勢。

▋Vertical AI 的機會與挑戰

市場潛力與效率優勢

Vertical AI 展現強勁成長動能，

市場規模預計從 2024 年的 51 億美元，

擴張至 2030 年的 471 億美元。

相較於水平供應商，垂直解決方案在營運效率上具備顯著優勢：

銷售與行銷成本僅佔營收 17%（水平供應商為 34%）。

LLM-native 垂直公司更展現年增 400% 的高速成長，

同時維持 65% 的健康毛利率。

實施挑戰與隱藏成本

然而樂觀數據背後存在嚴峻現實。

目前 70-85% 的 AI 專案未能達到預期成果，

專案放棄率更從 2024 年的 17% 激增至 2025 年的 42%，

顯示實施難度遠超預期。

成本控制困境： 

企業 AI 平均月支出增長達 36%，

實際部署成本通常是廣告訂閱價格的 3-5 倍，

因為需要涵蓋系統整合、客製化開發、基礎設施擴展，

及持續維運等隱藏開銷。

成果定義模糊： 

Zendesk outcome-based pricing 遭遇成功解決定義的歧義，

當客戶點擊問題已解決，

但隨即再次提問時，該如何計費？

這類模糊地帶直接影響收費模型的可行性與客戶滿意度。

Vertical AI 雖具備結構性優勢，

但成功關鍵在於建立清晰的成果衡量標準、透明的成本結構，

以及務實的客戶期望管理。

[ 第二部分: 為你的 AI 產品定位 ]

本部分要釐清 AI 產品定位，

在「水平、垂直、正交」市場間抉擇，

並權衡流程中心 (SaaS-first)與成果中心 (AI-first)的設計策略，

以上的釐清會關乎學習標竿、商業模式...等。

LLM 研究關鍵字： 

Horizontal/Vertical/Orthogonal Market、AI-first vs. SaaS-first、Outcome-based Pricing (RaaS)、Selling the Work、Agentic Workflow。

▋找到你的產品定位：從市場切入角度開始

在思考 AI 產品策略時，

第一步是釐清你要切入的市場屬性。

市場大致分為三種：

Horizontal（水平市場）：

這是跨產業、跨職能的通用工具，解決所有人都有的共同問題。

想想 Slack 讓所有公司都能更好地溝通、Zoom 讓所有人都能開視訊會議、Google Drive 讓所有人都能協作文件，這些工具不分產業，人人都需要。

Vertical（垂直市場）：這是專為特定產業量身打造的解決方案，深入該產業的法規、流程與獨有數據。比如牙醫管理系統要處理健保申報和病歷格式、營造業估價軟體要懂工程規範和材料成本，這些邏輯只有該產業用得到。

Orthogonal（正交市場）：這是跨產業但專為特定職能或角色打造的模式，服務的是不同公司裡的「同一群人」。Cursor 服務所有寫程式的工程師、Figma 服務所有做設計的設計師，不管你在什麼產業，只要你是這個角色，就需要這個工具。

▋SaaS 和 AI 思維框架：你想賣什麼?

確認市場屬性後，接著要決定產品的核心價值主張。

目前主流有三種思維：

SaaS + AI（賣更好的工具）：

在既有軟體中加入 AI 功能，讓人類更有效率地完成工作，

按軟體席位收費，瞄準的是企業軟體預算。

值得一提的是，

即使是水平 SaaS 也開始出現先為特定產業打造 Agent 的模式。

Vertical AI（用軟體直接賣服務）：

針對特定行業打造的 AI 原生應用，

直接完成原本需要人力處理的任務，

按工作成果收費，瞄準的是企業人力預算。

簡立峰觀點（做軟體是為了賣服務）：

Software 是工具，Service 才是目標。

台灣可以買別人的軟體、發展自己的服務，

或自己打造軟體與服務，但不管運用哪一種方式，

都必須以「服務」為最終目標。

台灣有硬體優勢，軟體可以外購，但服務要自己掌握。

這三種思維的差異在於：

前兩者是美國創投從「市場規模」切入，簡立峰是從「台灣產業定位」切入。

▋SaaS-first vs. AI-first：你的產品邏輯是什麼?

釐清賣什麼之後，還要決定產品的設計邏輯：

SaaS-first（傳統軟體思維）以流程為中心：

出發點是把工作流程標準化、可視化、可治理（權限/稽核/一致性），

核心價值是穩定的資料與流程底盤。

人機關係上，人是司機，軟體是工具；

人操作，系統加速與留痕。

介面特徵是表單、選單、Dashboard、工單/簽核流程。

AI-first（Agent 思維）以成果為中心：

出發點是讓 AI 直接完成任務並交付成果，

例如寫文案、整理報告、產生程式、執行操作。

核心價值是智能輔助加上部分自動行動。

人機關係上，人是主管，AI 是員工；

人下目標與規則，AI 執行並回報。

介面特徵是對話/自然語言加上背景編排；

但仍需可控、可追溯、可介入。

一句話差異：SaaS-first 讓流程更清楚，AI-first 讓流程更少需要人操作。

▋實際案例：不同定位的 AI 產品

看完理論，來看實際案例會更清楚：

Vertical AI Agent - Anthropic + 金融領域：

雖然 Anthropic (Claude) 本身是水平的模型，

但與金融機構合作，針對銀行合規、金融審查、

詐騙偵測進行微調或結合產業特定數據時，

它就變成了 Vertical AI，

解決的是金融業獨有的專業任務。

Horizontal + Vertical Agents - Salesforce + Agentforce：

Salesforce 本身是水平平台（CRM），

但它推出的 Agentforce 讓企業可以快速建立垂直任務的 Agent。

例如專門處理保險理賠的 AI、專門做醫療預約的 AI，

它是用水平的技術架構來支援成千上萬個垂直應用。

Orthogonal AI Agent - Cursor / Claude Code：

Cursor 針對「開發者」這個角色，

無論你在哪種產業寫程式，它的功能都一樣強大，

它在 AI-first 時代重新定義了 IDE。

Claude Code (CLI) 是 Anthropic 推出的終端機 Agent，

同樣是針對開發者，能理解整個 Codebase，

直接進行多檔案重構與 Debug，

這是不折不扣的「正交 AI」。

▋Agent 的三種實現模式

確認產品定位後，接著要選擇 Agent 的實現方式：

模式一：工具 + Agent 讓效率極大化：

目前軟體開發 Agent 算是非常成功，

像 Cursor 等各家開發軟體都有一定客群，

另外有 Claude Code 這種你自己電腦小精靈模式。

除了軟體開發，其他專業軟體應該也可以有類似想像，

例如 AutoCAD + Agent。

模式二：SaaS + Agent：

原本就有成熟 SaaS 服務，

在此基礎上衍伸出工作流基礎的 Agent，

甚至有少部分服務開始嘗試用完成的成果數量來收費。

例如 Intercom Fin、Salesforce Agentforce。

模式三：Vertical AI - 從協作工具進化為「成果交付」：

目標是實現 Job Done（全責交付），

這類 AI 深入特定產業的護城河（數據、法規、專用格式），

並具備實質的品質稽核與風險控管能力。

第三種模式的核心特質包括：

高合規與高精度，處理大量專有數據（數倉、病歷、法規），

並能精準回溯來源；封閉式工作流，

輸出最終產出（如索賠文件、計費代碼），

不是對話建議；

商業模式有機會從賣帳號轉向賣成果（Selling the Work）。

▋Vertical AI 的領域應用實例

看幾個實際在運作的 Vertical AI 案例：

專業文書與決策支援領域：

金融分析方面，Anthropic 與金融服務業合作，

整合內部數倉與外部市場資料，

直接產出符合業界規範的投資研究報告或財報模型，

實現數據到交付物的自動化。

建築法規方面，

UpCodes AI 將模糊的設計需求轉化為具體的法規條文比對，

提供具備法律基礎的合規性檢索。

高價值法律與理賠交付領域：

法律科技的 EvenUp (Demands™) 展現了「產出即價值」的典型，

交付可直接提交給保險公司的索賠建議包，

透過 AI 加上人工審核確保和解金額極大化。

車損理賠的 Tractable 透過電腦視覺進行損害評估，

將傳統需數天的估損動作壓縮至分鐘級，

交付的是修繕決策而非影像分析。

醫療流程與收入循環管理領域：

臨床筆記的 Abridge 解決醫護痛點，

將醫病對話轉為可計費、可寫入 EMR 的正式病歷，

這不只是紀錄，而是診所營運的核心資產。

醫療編碼的 CodaMetrix 是收入門戶的極致體現，

將複雜臨床紀錄精準轉化為醫療編碼（Medical Coding），

直接影響院方的收入週期（RCM）。

▋Vertical AI 判斷標準

分析一些 Vertical AI 案例可找出共同特性，

1. 高專業門檻與合規要求

．需要深度領域知識（金融法規、建築規範、醫療編碼）

．有明確的產業標準或法律規範

．錯誤成本極高，需要精準度保證

2. 從非結構化到結構化的轉換

．輸入：模糊需求、對話內容、影像資料

．輸出：符合規範的文件、編碼、決策建議

．核心價值在於「標準化」與「可稽核性」

3. 直接影響企業財務指標

．金融：投資決策、財報產出

．法律：和解金額極大化

．醫療：計費編碼（直接影響收入）

．都是「影響錢」的關鍵環節

4. 大量專有數據與系統整合

．需整合內部數倉、EMR、歷史紀錄

．結合外部資料（市場數據、法規庫）

．不是單純的 AI 推論，而是「數據 + 邏輯 + AI」

5. 時效性帶來的競爭優勢

．從「數天」壓縮到「分鐘級」

．從「人工整理」到「即時產出」

．速度提升直接轉化為商業價值

6. 可交付的最終產出（非建議）

．不是「給你參考」而是「可直接使用」

．索賠包可直接提交、病歷可直接寫入系統、報告符合監管要求

．輸出物本身就是工作成果

▋成果定價的現實挑戰

如果你選擇按成果收費，要知道這條路充滿挑戰。

含結果元素的公司毛利率比純 usage-based 高，

但 24-25 年期間只有不到 15% AI-native 公司採用成果定價，

以上案子接近一半都在實驗階段。

Salesforce Agentforce 推出沒多久，

就從 per-conversation 退回 seat+usage 混合模式。

真相是：

客戶想買成果，但更想要成本可預測性。

數據顯示 55% 採用 AI 後裁員的公司後悔此決定（Forrester）、

58% 企業認為 cloud 成本過高且 AI 只會加劇、

企業要的是 financial certainty 不是 unlimited innovation。

主要風險包括：

歸因爭議（Zendesk 案例：AI bot 回覆後客戶短期內又回來,算 resolved 嗎？）、

成本失控（在調整定價的公司中，40% 沒看到客戶對齊度改善）、

會計複雜性（ASC 606 要求區分 access vs delivery，影響 revenue recognition）、

客戶承受度（70% 高管因成本取消或延遲至少一個 GenAI 專案）。

▋正在運作的定價模式

目前有些模式正在證明可行：

．Intercom Fin ： $0.99/解決加上嚴格定義解決標準。

．Sierra 以 Outcome-based 為主，但提供 blended approach。

．Decagon 採用 per-conversation（usage），加上 per-resolution（outcome）雙軌。

．新興模式是 Burstable reserve（固定基準價加上超量按 outcome 計費）。

▋長期需要探索的方向

如果你決定走成果定價這條路，長期需要投入的包括：

結果定義的工程化：如何建立 golden set、sampling 機制、human-in-loop review？

風險分擔機制：如何設計 performance guarantee 但不讓自己吃掉所有 downside？

從結果回推的產品策略：如果收入綁定成果，你的 product roadmap 邏輯會完全改變。

總結來說，找到你的 AI 產品定位需要回答三個核心問題：

你要切入哪種市場（Horizontal / Vertical / Orthogonal）？

你想賣什麼（工具 / 服務 / 成果）？

你的產品邏輯是什麼（SaaS-first / AI-first）？

這些選擇會決定你的技術架構、商業模式、甚至團隊組成。

[第三部分: AI Agent in Databricks ]

探討以 Databricks 為核心的 AI 產品開發路徑，

分析其作為水平平台、正交工具與垂直賦能者的多重定位。

透過「數據、策略、互動」三層架構，

引導系統從資訊萃取演進至自動化 Agent，

並以零售廣告 (RMN) 為例，

說明如何將底層 Lakehouse 轉化為，

解決特定產業問題的「垂直領域 AI (Vertical AI)」。

最終目標是在確保企業級治理 (SaaS-first) 的前提下，

實現以成果為導向 (AI-first) 的自動化執行，

完成從「賣工具」到「賣成果 (Selling the Work)」的商業模式轉型。

LLM 研究關鍵字：

Databricks Multi-positioning (Horizontal/Orthogonal/Vertical)、3-Layer Architecture (Data/Strategy/Interaction)、Pipeline-to-Agent Evolution、Vertical AI (Retail Media Network)、SaaS-first vs. AI-first (Governance vs. Outcome)、Selling the Work (Job Done)、Action-based Pricing。

▋理解 Databricks 的特殊定位

Databricks 在產品分類中具有多重身份，

這讓它既是基礎設施，

也是應用賦能者：

Horizontal (水平市場) — 平台本質：

Databricks Lakehouse 本身是跨產業、跨職能的，

無論金融、醫療或零售業，

都需要資料治理 (Unity Catalog) 與運算資源。

這是它的底層特性。

Orthogonal (正交市場) — 職能深耕：

針對「資料工程師」與「資料分析師」開發的 AI 助手，

例如 AI/BI Genie、自動產生 SQL，

即是典型的正交模式。

它服務於不同公司裡的同一群人，

讓這些專業角色的工作流程發生變革。

Vertical Enabler (垂直市場賦能者)：

Databricks 本身不直接賣牙醫系統，

但透過 Marketplace 與加速器方案（如 AstraZeneca 臨床試驗解析），

它讓企業能快速產出 Vertical AI。

▋用 Databricks 建產品的三層架構思維

當你用 Databricks 作為產品核心時，

需要理解三層架構如何共同決定最終價值：

第一層：基礎系統層（業務數據來源）：

這是原本的業務系統，

是 Databricks 的數據來源。

它的任務是將業務邏輯沉澱成可靠的數據記錄，

把 Rules 轉成可追溯的事實 Data。

這一層決定「能回答哪些問題」，

資料是否可靠、齊全、可追溯。

第二層：策略分析層（Databricks 數據中心）：

這是 Pipeline + Business Data Science 的核心。

從數據中萃取意義、建立指標、做預測與歸因，

讓 Data 經過整理後更能連結決策（更可讀、更可比、更可用）。

這一層決定「回答有多有洞見」，

萃取、指標、模型、推論品質。

第三層：互動 AI 層（GenAI / Agent 功能）：

這是 mediate between Data and User 的過程。

GenAI 提升理解與使用效率（問答、摘要、解釋、建議、報告），

Agent 把理解/建議接到流程動作，

推進到可交付的成果。

這一層決定「價值能否被用戶真正接收與用起來」，

從理解到行動到成果。

▋Pipeline、GenAI、Agent 的演進關係

理解三者的關係，

關鍵在於看清它們如何逐步推進「系統與人的關係」：

Pipeline（聽話階段）：系統是工具，人下指令。

數據中心的分析型/預測型 AI 重點在「萃取資訊」，

讓數據變得更容易支援決策。

這階段著重在把原始數據轉換成有意義的金質 table。

GenAI（說話階段）：系統提供洞見與建議，人做決定。

GenAI 讓數據（包含萃取後的金質 table），

更容易被使用者理解、使用，進而完成業務。

它提升的是「數據到理解」的效率。

Agent（對話階段）：

人和系統一起釐清目標、來回探索，逐步得到答案；

在授權下也能代辦部分任務。

Agent 讓數據可以更直接推進到「業務成果」，

真正實現從理解到執行的閉環。

重點方向：先把資料與互動方式規劃好，才能替未來 Agent 鋪路。

▋Data ↔ User 雙向互動的三種型態

當你規劃 GenAI 和 Agent 功能時，

要理解這個雙向性同時涵蓋：

被動回應：用戶問，系統答。

這是最基礎的 GenAI 應用，

例如「這週哪些店表現最好？」系統根據金表直接回答。

主動推送：系統偵測，用戶接收。

系統發現異常或機會時主動通知，

例如「A 店午餐時段轉換率突然下降 30%」。

協作探索：來回對話逼近需求與決策。

人和 AI 一起討論「為什麼下降？該怎麼調整？」

並逐步形成行動方案。

AI Agent 的各種形態，可以視為「雙向互動」的不同實作方式與成熟度。

▋具體案例：商店螢幕廣告「午餐檔期」優化

用一個完整例子來理解三層架構如何協作：

數據中心層（Databricks Pipeline）：

把「播放紀錄 + 人流/停留 +（可選）銷售」整理成金表，

每家店每時段的「曝光、看完率、有效停留、成本、轉換指標」都清楚記錄，

並算出「最佳受眾包 × 最佳素材」建議清單。

GenAI 層（讓人更快用得上）：

PM/Sales 問「這週午餐時段哪 10 家店最值得加碼？為什麼？」

GenAI 直接用金表生成：

Top 店點清單 + 3 個理由 + 風險提醒（例如樣本不足）+ 一段可貼給客戶的摘要。

Agent 層（直接交付成果）：

使用者一句話「把 Top 10 店午餐時段改播 A 素材，

預算維持不變，跑 7 天」，

Agent 自動：建立投放計畫 → 呼叫 CMS 排程上架 → 設定 A/B 與成效門檻 → 每天回報 → 低於門檻就降載/換素材 → 結案產出報告。

▋基於 Databricks 的產品定位策略

結合 Databricks 的技術特性與「Databricks + 應用層」的架構，

產品定調可以這樣思考：

1. 產品市場定位：垂直領域 AI (Vertical AI)：

雖然底層 Databricks 是水平平台，

但產品透過應用層封裝了零售與 RMN 的特定業務邏輯，

應定位為 Vertical AI。

核心價值在於深入零售業數據特徵（如 POS、人流、看板紀錄），

解決產業特有的廣告歸因與精準投放問題。

Databricks 特性結合：

利用 Lakehouse 統一架構處理 RMN 複雜的結構化（交易），

與非結構化（影像分析）數據，

打破零售業常見的數據孤島。

2. 思維框架：從 SaaS + AI 進化至 Vertical AI：

產品不只是提供「更好的工具」，

而是旨在「直接交付成果」。

SaaS + AI (工具層面) 提供儀表板與數據管理，

按軟體席位或 DBU (Databricks Unit) 運算量收費。

Vertical AI (服務層面) 目標是直接完成原本需要行銷人員執行的「廣告排程優化」，

或「受眾細分」。

簡立峰觀點：軟體（Databricks + App）是工具，

最終賣的是零售場域的「數據服務與自動化決策」。

3. 產品設計邏輯：雙軌制 (SaaS-first + AI-first)：

針對企業級客戶，

產品必須同時具備「可控流程」與「智能成果」。

SaaS-first (流程中心) 依賴 Unity Catalog 提供數據治理、權限控管與審計追蹤，

人是司機，系統負責穩定的數據管線與安全合規。

AI-first (成果中心) 整合 AI/BI Genie 與 Agentic Workflow，

人是主管，AI Agent 負責數據洞察與自動化執行。

4. Agent 實現模式：模式二至模式三的跨越：

模式二 (SaaS + Agent) 基於 Databricks 穩定的數據底座，

發展出輔助操作的 Agent。

模式三 (Vertical AI) 邁向「成果交付」，

例如透過 Mosaic AI 微調零售專用模型，

直接產出高精度的索賠/廣告效果包，

實現 Job Done 的目標。

▋商業模式與定價策略考量

針對「部署到客戶環境」或「SaaS」的不同路徑，應對方案如下：

部署靈活性：

利用 Databricks 的雲端原生特性，

支持 VPC 部署，

滿足大型客戶對「數據主權」的高合規要求。

定價策略：

基礎層採用 Usage-based (DBU) 或訂閱制，確保成本可預測。

加值層探索 Burstable Reserve，

針對 AI 產出的「成功歸因數」或「自動優化次數」進行階梯式計費。

風險控管：

利用 Databricks 的監控工具建立 Human-in-the-loop 機制，

解決 AI 成果歸因爭議。

▋護城河建設的三個關鍵

數據資產：

累積行業專有數據，這是最難複製的競爭優勢。

工具鏈整合：

Databricks + Unity Catalog + Vector Search 形成技術護城河，

確保系統穩定性與擴展性。

專業服務：

不只提供工具，

還提供顧問和優化服務，

從「賣平台」進化到「賣成果」(RaaS)。

▋定價參考對標對象

找到合適的對標對象可以幫助你設計定價模式：

Ad2：

學習受眾/創意/優化模組怎麼切、怎麼商品化，這是功能/AI 模組能力的參考。

Dataiku / GitLab Duo Self-Hosted：

學習私有環境/On-Prem 部署模式，客戶出 token、供應商收模組授權 + 用量。

Dataiku 是 Low Code Self-Hosted（可部署於地端或私有雲）平台，

重點在於數據處理的流程編排與團隊協作，

沒有儲存跟運算資源，

可以跟 Databricks 串接。

收費採平台授權費 (SaaS/On-prem License)，年費，

提供席次+不同進階功能。

Intercom Fin / Salesforce Agentforce：

學習 Agent 計價法/行為單位，

不收 token 而是收 action / 事件 / 成果。

Intercom Fin 是 SaaS，

AI 問答功能按件計酬，每成功解決一次問題 $0.99 美元。

最準確的 benchmark 是:

Ad2（方向）× Dataiku（部署模式）× Salesforce/Intercom（Agent 計費方式）

的組合參考。

[ 部四分：領域現況與競爭態勢調研 ]

本部分透過調研數位看板與 RMN 市場，

將功能模組化為「基礎、分析、Agent」三層級。

目的在於協助讀者識別市場現狀，

並透過「F.D.A. 框架」找出 AI Agent 開發題目。

LLM 研究關鍵字：

Retail Media Network (RMN), DOOH Analytics, Proof-of-Play (PoP), Data Clean Room (DCR), Multi-sensor Fusion, Conversion Attribution, Agentic Workflow in AdTech.

▋ 尋找高價值 Agent 的方法論：F.D.A. 框架

1.Friction (摩擦點)：

尋找高頻、重複且需「人工審核」的環節

（如：素材規格與合規檢查）。

2.Data Nexus (數據交匯)：

鎖定非結構化數據的交匯點（如：Camera 人流影像 + POS 銷售明細）。

處理「數據交叉後的決策」最值錢。

3.Actionable Outcome (可執行的成果)：

評估該功能是否能從「給圖表」進化到「交付工作成果」

（如：自動產出結案報告）。

▋ 店內電子螢幕廣告分析：功能優先級全清單

一、 一般系統功能（基礎底盤：確保穩定運作與交付）

．多螢幕內容排程與派送｜市場：高｜成熟：高｜代表：Broadsign

．網路監控與播出證明 (Proof-of-Play)｜市場：高｜成熟：高｜代表：Broadsign Control

．對外整合能力 (API/SSO/POS 串接)｜市場：高｜成熟：高｜代表：SpinetiX HUB

．權限、稽核與單一入口 (RBAC/Audit)｜市場：高｜成熟：高｜代表：SpinetiX HUB

．內容素材庫、模板與品牌控管｜市場：中｜成熟：高｜代表：ScreenCloud

二、 分析或非 Agent 的 AI 功能（洞察輔助：找線索、講清楚）

．自動洞察摘要 (AI 解讀指標原因)｜市場：高｜成熟：中高｜代表：Tableau Pulse

．指標異常偵測＋解釋 (KPI Anomaly)｜市場：高｜成熟：中高｜代表：Tableau Pulse

．多感測器/多資料源融合分析 (Camera+POS)｜市場：高｜成熟：中｜代表：RetailNext

．人群型態自動分群 (Audience Discovery)｜市場：中高｜成熟：中｜代表：Vistar

．內容影片解析與自動貼標｜市場：中高｜成熟：中｜代表：Broadsign

三、 Agent 功能（全責交付：幫你完成一段工作流程）

．素材 QA / 審核 Agent｜市場：高｜成熟：中｜自動化分類與合規檢查。

．Chat with Data (自然語言問答)｜市場：高｜成熟：中高｜代表：Power BI Copilot

．成效/實驗設計 Agent (Privacy-safe)｜市場：中高｜成熟：低｜代表：Snowflake Clean Room

．投放/排程規劃 Agent (Planner)｜市場：中｜成熟：中｜代表：Hivestack

．維運 Agent (異常處置建議/自動派工)｜市場：中｜成熟：中｜代表：Broadsign Control

．動態內容觸發設定 Agent｜市場：中｜成熟：中｜代表：Broadsign DCO

[第五部分: 規劃 Agent 功能   ]

本部分探討 AI Agent 的技術選型邏輯與任務適配標準，

旨在避免盲目使用 Agent 導致的維運高成本與低穩定性。

首先區分「純程式碼、工作流、RAG、Agent」的適用邊界，

強調 Agent 核心價值在於處理高度變動輸入與自主多步推理。

接著提出一套客觀的「Agent 化適配指標」（Scorecard），

從規則明確性、結果可驗證性、回饋延遲等維度評估任務的自動化潛力。

最後定義了 Agent 的七種常見形態（如業務任務型、分析型、領域專用型等），

並以程式開發為標竿，指出具備「狀態空間可模擬性」與「自動驗證閉環」的領域，

才是 AI Agent 能產生最高 ROI 與護城河的戰場。

LLM 研究關鍵字：

Agent Selection Matrix (Code/Workflow/RAG/Agent)、Task Verifiability、Agent Scorecard、7 Agent Archetypes (Business/Analytics/Domain-specific, etc.)、State Space Simulation、Feedback Latency、Logic Atomization、Formalization of Constraints、Human-in-the-loop (HITL) Gateways。

▋什麼時候該用真正 Agent：四種技術選型的判斷

到底該用純程式碼、工作流、RAG 問答、真正的 Agent？

不是每個需求都該上 Agent，選錯會變成又貴又難維運。

以下分類：

Traditional code（純程式碼）：

適用於輸入很固定、規則可完全寫死、需要超低延遲或高可稽核的場景。

例如固定格式的 log 解析、感測器即時控制、金融/醫療某些必須「完全可解釋」的判斷。

重點是最便宜、最快、最好測試，但不會處理模糊需求。

Workflow（確定分支的工作流/流程引擎）：

適用於步驟清楚、分支有限、你能列出所有例外與人工審核點的情況。

例如發票處理（CSV/JSON/PDF 三種格式→走不同 parser→對帳失敗就停下來請人審）。

重點是可控、可追蹤、可治理；比 Agent 穩定，

但遇到「新花樣輸入」會很脆。

Chatbot / RAG（文件問答系統）：

適用於主要是「查資料、讀文件、回答問題」，

不需要它自己去做事的場景。

例如 IT helpdesk 問「怎麼重設 VPN」，

系統去找內部指南並整理成步驟。

重點是它「會回答」，

但通常不會自主決定下一步行動

（不會自動開單、改設定、發信⋯⋯除非你再加 workflow/工具）。

Autonomous agent（真正的 Agent）：

適用於輸入高度不固定、需要多步推理與規劃、會因中途結果而改計畫，

還可能並行做多件事的情境。

例如客服信件千奇百怪、供應鏈遇到突發狀況要重排、

SOC 要同時查威脅情報/查 log/做隔離建議。

重點是它「會想、會決定、會動作」；

但代價是成本高、治理與評估更難、維運更辛苦。

▋選型判準：最核心的 4 個問題

在決定是否採用 Agent 之前，先問自己這四個問題：

輸入是不是高度變動/不結構化？

是不是需要多步規劃，而且會根據中途結果改變下一步？

是否真的需要自主呼叫外部工具去「做事」？

你能不能承受更高的延遲、成本、與維運治理負擔？

值得上 Agent 的產品選題應該要找：

RAG 解不了（只回答不夠）、

workflow 太脆弱（例外太多）、但又能把 outcome 定義清楚、

可稽核、可計價。

這就是「大公司吃不到、願意付錢、做得出來」的交集點。

▋AI Agent 優先順序比較指標

以下指標可作為 scorecard 篩選標準，

用來判斷某個任務或工作是否值得開發 AI Agent 

或自動化解決方案：

1) 任務規則明確性（Task Definition Clarity）：

任務是否由明確步驟、可形式化、可拆解為規則或算法？

即使是複雜決策，

也需能定義判斷標準、邊界條件與成功標準。

任務規則越明確可形式化，

越適合自動化或 agent 執行。

2) 可重複性/高頻率（Repetitiveness / Frequency）：

執行次數是否頻繁？

同類型任務是否大量存在？

重複性高使得 agent 能夠透過統計模式與策略優化自身行為。

如果任務每天重複或在多個用例中重複出現，

自動化價值高。

3) 結果可驗證性（Outcome Verifiability）：

是否有明確的成功/失敗判準，

可透過測試、對比或驗證器自動評估結果？

和編譯器/unit test 類似，

agent 執行後能否判斷是好是壞。

可生成 guardrails、sandbox testing、反饋回路。

4) 資料完整性/豐富度（Data Availability & Quality）：

是否存在高質量輸入輸出數據、歷史 log、標註 examples？

可用於訓練、驗證、自我改進與演化。

資料越可得，

AI 代理學習與優化越穩健。

5) 可量化的 KPI/成果（Objective Metrics）：

是否有明確的 KPI（如錯誤率、處理時間、成本節省率、準確率等）？

量化目標能讓 agent 的成效更客觀對比。

成果可度量才容易驗證與 ROI 計算。

6) 風險與信任要求（Risk / Safety Constraints）：

是否能在 agent 決策過程中控制風險？

若錯誤成本極高（如金融交易、飛行控制），

需要額外人機協作設計。

風險高但可分級，

仍可以 agent 介入某些子任務。

總結:

A. 高優先自動化（Agent 自主決策）：

適合開發 AI Agent 的任務通常具備：

高重複性且流程可拆解、明確成功/失敗判準、

大量輸入資料可供推理/學習、

可建立 feedback loop 驗證效果、低到中等風險（或可漸進引入 human-in-loop）。

例如自動化報表比對、

基於規則的決策支持、自動分類與歸檔、

結構化事件判定與 routing。

B. 次優自動化（需要人機協作）：

任務雖重要但因多變與不確定而不建議完全交由 AI 自動執行：

需要大量常識推理、彈性協商、

需要理解隱性知識（Polanyi's paradox 問題）。

例如創意策略制定、

需要社會情境判斷的溝通決策、

高風險金融/醫療決策（需 human oversight）。

▋Agent 7 種常見型態分類

理解不同 Agent 型態可以幫助你更精準地定位產品方向：

1) Business-task Agents（業務任務型）：

把既有的流程自動化，

接到事件 → 執行一串動作（開單、更新狀態、寫入系統、通知人）。

特點是「可控、可稽核」，適合高頻、規則明確的流程。

2) Conversational Agents（對話型）：

以聊天介面承接需求、回覆問題、引導下一步。

它的價值多半在「入口與體驗」，但不等於真的能交付成果。

3) Research Agents（研究型）：

負責找資料、讀文件、整理重點、產出可引用的結論。

常見於研究、法務、投研、內部知識查詢，核心是「蒐集 + 濃縮 + 引用可追溯」。

4) Analytics Agents（分析型）：

對結構化數據做解釋與洞見輸出，

像是用自然語言查數倉、產出指標解釋、協助生成報表與結論。

特別適合「數據中心（例如 Databricks）+ 應用層」的產品形態。

5) Developer Agents（開發型）：

在 IDE/Repo 工作流中協助寫碼、改碼、測試、Review。

通常是提升效率的「工具型 Agent」，商業模式容易落在 seat / subscription。

6) Domain-specific Agents（領域專用型）：

針對特定職能/產業流程（法務、醫療、金融、理賠⋯⋯）

把專業知識與交付物格式封裝起來。

這類最接近 Vertical AI：價值不只是回答，

而是能進入 workflow、產出可用交付物。

7) Browser-using Agents（瀏覽器操作型）：

能在網站上「看懂畫面、點擊、填表、抓資料」並完成任務。

比傳統 RPA 更能應付例外狀況，

但治理與風險控管也更重要。

▋重要潛力：類程式開發的高度可 Agent 化領域判定標準

要評估一個領域能否像程式開發一樣，

被 AI Agent 高效自動化，

可從五個核心維度來判斷:

一、狀態空間的可模擬性

該領域能否在數位環境中精準模擬?

若能在不介入物理世界的情況下完成試錯，

強化學習的訓練效率將呈指數級增長。

程式開發之所以成為 AI Agent 的理想戰場，

正是因為整個開發環境都可以在沙盒中完整重現。

二、回饋延遲性

從模型輸出到獲得對錯訊號的時間有多長?

程式編譯僅需秒級，

而藥物實驗可能需要數月甚至數年。

延遲越低，

閉環優化的速度就越快，模型進步的週期也越短。

三、規則與約束的可形式化程度

規則能否寫成語法、DSL 或約束條件?

能用 SQL、表單規則、狀態機或 constraint 明確表達的領域，

天生就更適合 Agent 化。

同時需要考慮:

需求的歧義度(不同人執行結果是否高度一致)，

以及邊界條件能否被系統化列舉(例外少、容易窮舉，自動化可靠度高)。

四、可驗證性與回饋閉環

關注三件事:

首先是自動驗證器是否存在，

也就是有沒有等價於 compiler 或 unit test 的東西，

像是 validator、simulator、golden set 或 reconciler。

其次是失敗能否被精確定位，

錯了能不能指出是哪條規則、哪個步驟出問題。

最後是回饋速度，

從產出到驗證的延遲是秒級分鐘級(像跑測試)，

還是天級週級(像要等人工審核)。

五、高品質資料與標註可得性

理想的領域應該擁有大量的 input-output 配對資料，

例如歷史工單、報表、對帳結果、審核結論或配置變更紀錄，

資料分布要相對穩定(規則和流程變動的頻率越低越好)，

並且最好能從系統日誌自動產生標籤，

像是「部署成功或失敗」、「對帳差異為零」、「測試通過」這類訊號)，

以大幅降低標註成本。

程式開發為何是最佳範例? 

因為它在每個維度上都表現優異:

有 BNF 文法定義這樣形式化的規則體系;

編譯通過、測試通過、效能數據提供了明確的驗證手段;

GitHub 上數十億行開源程式碼構成了龐大的訓練素材;

而「能跑就是對的」這個簡單判準讓結果導向性極為明確。

增強潛力的加分條件還包括:

邏輯原子化:

。任務能否被拆解為具備明確輸入、輸出與副作用的獨立模組，就像 Function 或 Microservices 的設計理念

。迭代成本低(試錯快速、回饋週期短)、

。既有的自動化基礎(linter、formatter、validator 這些工具鏈都可以直接複用)

。專家行為可追蹤:

專業人士的操作過程有數位足跡可供學習

。錯誤影響可控:

失敗不會造成不可逆的災難,或至少可以在沙盒中隔離測試

[第六部分: 實現 Agent 的技術棧 ]

本部分詳解 AI Agent 的技術實現路徑，

將其抽象為「大腦（模型）、記憶（上下文/RAG）、手（工具）與神經網路（編排）」

四大核心組件。

內容對標了主流雲端平台（如 Databricks Mosaic AI 與 AWS）的服務映射，

並強調生產級 Agent 的成功在於 95% 的周邊工程：

包含上下文工程 (Context Engineering)、

評估體系 (Evals)、

彈性架構與成本治理。

針對 2025 年的技術趨勢，

提出「從深且窄」的產品策略，

並點出未來競爭力在於如何將模型輸出轉化為穩定、

可控且具備「主見 (Opinionated)」的業務成果交付。

LLM 研究關鍵字：

Agentic Workflows, Brain-Memory-Hands Architecture, Context Engineering (Selection & Validation), Tool Calling & Registry, Orchestration (LangGraph/StateGraph), Mosaic AI Agent Framework, MCP (Model Context Protocol), LLM-as-a-judge, Model Routing, Resilience & Error Handling, Opinionated AI (Outcome-driven).

▋Agent 擬人的抽象組成

Agent 系統通常被類比為一個具有行為能力的個體，

其核心抽象組件包括：

大腦 (The Brain / Model)：

核心決策引擎。負責解析意圖、邏輯推理、

計畫拆解以及最後的語言生成。

記憶 (Memory)：

短期記憶是當前對話的上下文（Context Window），

讓 Agent 記得剛才說過什麼。

長期記憶存儲過去的經驗、用戶偏好或專業知識庫。

手 (Hands / Tools)：執行能力。

Agent 透過「工具調用 (Tool Calling)」與現實世界互動，

如查詢資料庫、發送郵件。

神經網路/編排 (Orchestration)：

連接大腦、記憶與工具的邏輯流，

決定 Agent 如何根據環境變化調整行動路徑。

▋Agent 服務與工具組成

大腦：LLM 技術與計畫：

模型選擇分為旗艦模型 (Flagship) ，

適合同時處理複雜推理、多步規劃；

以及小模型 (SLM) ，適合單一、高頻率、低延遲任務（如客服取消訂單）。

規劃 (Planning) 透過 StateGraph (如 LangGraph) ，

或 Plan-and-Execute 模式，

將任務拆解為子目標。

記憶層次：

短期記憶使用 Rolling Context Windows，動態丟棄過時資訊，保持 Prompt 效率。長期記憶包含 RAG (知識庫) 使用向量資料庫儲存文件知識、User Profile 存儲用戶個性化設定、MCP (Model Context Protocol) 是一種新標準，允許 Agent 直接將外部狀態（如即時數據）注入大腦推理過程，減少工具調用的往返。

工具與功能 (Functions)：

Local Tools 是內部的程式邏輯（如數學運算）。API-based Tools 串接外部服務（如 Stripe 退款 API、Salesforce CRM）。

▋ Agent 開發前的準備：實務規劃

在進入開發階段前，建立穩固的底層邏輯與驗證基準是成功的關鍵。

數據、功能與 API 基礎：

數據整備需區分非結構化數據（如文件、Wiki）的清洗分段，以及結構化數據（如資料庫欄位）的語義標註。工具設計應遵循原子化原則，確保每個 Function 職責單一。API 則需建立安全沙箱環境，特別是涉及「寫入」操作的功能，必須設計人機協同審核機制以規避風險。

釐清流程與驗證路徑：

針對目標成果，開發者應先手動模擬決策流程，將黑盒子的推理邏輯轉化為可視化的路徑圖。建立「黃金集 (Golden Dataset)」是檢驗 Agent 表現的唯一標準，這包含了一組標準輸入及其預期的正確輸出，用於後續自動化評估工具的基準測試。

流程規劃與工具抽象化：

將複雜任務拆解為多個子目標，並為每個工具編寫精確的 Prompt 描述。LLM 是透過描述來理解工具的用途，因此語義的清晰度直接影響調用成功率。此外，需定義清晰的錯誤處理邏輯，當 API 失敗時，應回傳結構化的錯誤訊息引導 Agent 進行自我修正或嘗試替代路徑。

▋重要程序

1. Context Engineering (上下文工程)：

設計 System Prompt 定義 Agent 的角色、權限與行為準則。

利用 MCP 或動態檢索將正確的資料放入 Context。

2. LLM Fine-tuning (微調)：

當 Prompt Engineering 無法滿足特定領域（如醫療、法律）的準確度時，

使用特定領域數據進行微調。

3. 成果評估 (Evaluation)：

功能測試確認是否調用了正確的工具、參數是否正確。

用戶體驗 (UX) 透過 NPS、CSAT 或隱含訊號（用戶是否採納結果）來評估。

自動化評估使用「模型評估模型 (LLM-as-a-judge)」來進行大規模測試。

4. 迭代設計 (Iterative Design)：從 MVP (最小可行性產品) 開始，例如文中提到的「僅自動化取消訂單」，穩定後再擴張。

▋ Agent 開發前的準備:實務規劃

在進入開發階段前，

建立穩固的底層邏輯與驗證基準是成功的關鍵。

數據、功能與 API 基礎:

數據整備需區分非結構化數據(如文件、Wiki)的清洗分段，

以及結構化數據(如資料庫欄位)的語義標註。

工具設計應遵循原子化原則，確保每個 Function 職責單一。

API 則需建立安全沙箱環境，

特別是涉及「寫入」操作的功能，必須設計人機協同審核機制以規避風險。

釐清流程與驗證路徑:

針對目標成果，開發者應先手動模擬決策流程，

將黑盒子的推理邏輯轉化為可視化的路徑圖。

建立 Golden Dataset 是檢驗 Agent 表現的唯一標準，

這包含了一組標準輸入及其預期的正確輸出，

用於後續自動化評估工具的基準測試。

流程規劃與工具抽象化:

將複雜任務拆解為多個子目標，並為每個工具編寫精確的 Prompt 描述。

LLM 是透過描述來理解工具的用途，

因此語義的清晰度直接影響調用成功率。

此外,需定義清晰的錯誤處理邏輯，

當 API 失敗時，應回傳結構化的錯誤訊息，

引導 Agent 進行自我修正或嘗試替代路徑。

▋ 非特定服務的工具組合

適用於跨雲架構或追求高度客製化的開源生態。

大腦 (Model):根據任務特性選擇合適模型。

Claude Sonnet 4.5 (2025年9月發布)在編碼任務表現最強，

SWE-bench Verified 達 77.2%。

GPT-5(2025年8月發布)則在數學推理(AIME 2025滿分)與醫療應用表現優異，

且成本較低(輸入便宜 2.4 倍,輸出便宜 1.5 倍)。

需要專注推理任務可選擇 OpenAI o3(最強推理模型)，

或 o4-mini(高效推理,成本更低)。

追求極致低延遲則可考慮透過 Groq 部署的 Llama 3.1 旗艦模型。

編排 (Orchestration):LangChain 適合快速原型與線性工作流，擁有豐富的整合生態。

LangGraph 專為複雜、有狀態的 Agent 系統設計，

支援循環、分支與狀態管理，

適合生產環境的多步驟工作流。

兩者常混用:

用 LangChain 快速建構組件，用 LangGraph 處理複雜邏輯。

CrewAI 則適合多 Agent 協作場景。

追求型別安全可選擇 PydanticAI。

記憶 (Memory):短期狀態存儲於 Redis，

長期知識用 Pinecone、Weaviate 或 ChromaDB 等向量資料庫實現 RAG 檢索。

手與工具 (Tools):利用 MCP (Model Context Protocol) 建立標準化的外部數據連接，

或透過封裝良好的 Python Functions 執行運算任務。

▋ AWS 上的工具組合

利用 AWS 完整的託管服務實現企業級的安全性與高可用性。

大腦 (Model):Amazon Bedrock 提供多型態模型選擇，

包含 Claude Sonnet 4.5、GPT-5(成本與推理平衡)與 AWS 旗艦模型 Nova(2024 新發布)。

可根據任務特性動態切換模型。

編排 (Orchestration):Agents for Amazon Bedrock 提供了自動化的編排流程，

複雜的長流程則結合 AWS Step Functions 進行狀態轉換。

記憶 (Memory):使用 Knowledge Bases for Amazon Bedrock串接 Amazon OpenSearch Serverless，

實現自動化的向量化與知識檢索。

手與工具 (Tools):以 AWS Lambda 作為工具執行的核心，

透過 IAM 權限控管 Agent 對 S3 或 DynamoDB 等資源的存取。

▋ Databricks 上的工具組合

以 Data Intelligence 為核心,將數據治理與 Agent 開發深度整合。

特別適合已採用 Databricks 的企業。

大腦 (Model):透過 Mosaic AI Model Serving 可調用 Claude、GPT-5 等商用模型，

或部署 DBRX、Llama 等開源模型，

並確保所有模型調用符合內部合規。

編排 (Orchestration):Mosaic AI Agent Framework 是核心，

它與 MLflow 深度整合，支援從開發到部署的完整生命週期追蹤。

2025 年推出的 Agent Bricks 可自動化優化 Agent 品質。

記憶 (Memory):Databricks Vector Search 提供與 Unity Catalog 管理的 Delta Table 自動同步的功能，

確保 RAG 數據的即時性與治理合規。

2025 年新版採用分離式架構,成本降低 7 倍。

手與工具 (Tools):Unity Catalog Functions 將 SQL 或 Python 函數直接註冊為 Agent 工具，

具備完整的 Data Lineage 數據血緣追蹤與權限管控。

Mosaic AI Tools Catalog 讓企業建立內部工具註冊表。

評估 (Evaluation):利用 MLflow 3.0(2025 重新設計)進行自動化打分，

支援跨平台監控，即使 Agent 部署在 Databricks 外部也能追蹤。

Agent Evaluation 提供 AI 輔助評估與人工審核介面。

特色:Databricks 在 2025 年整合了 Anthropic MCP 協議，

可在 Playground 直接測試，

並提供 UC Functions、Genie、Vector Search 的 MCP 伺服器。

▋關鍵能力收斂（超精要版）

Context Engineering：裁剪/選擇/驗證/可觀測（本質是上下文特徵工程）

Memory 設計：個人/團隊/組織分層 + 隱私界線

Orchestration：流程圖化、狀態管理、可重試、可回放、可並行

Tooling 工程：原生 SDK 控制力、工具契約、共享狀態（避免資料孤島）

Resilience：錯誤處理、子 agent 重試、失敗知識回填（告訴它哪些路走過）

RAG 實戰：不是堆索引；要做訊號設計、檢索品質、結果驗證

Evals/Testing：建立回歸集、失敗分類、線上回饋迴圈（最難但最重要）

Model Routing：依難度/延遲/成本選模型，且能持續優化策略

產品設計觀：少選項、強主見、人機協作、從窄深任務打穿

[第七部分: 實戰與案例 ]

▋ 案例一：AWS 應用層 -「社群行銷創意自動化 Agent」

這個 Agent 的定位是「內容生產與發佈的操盤手」，

目標是讓品牌主從繁瑣的素材製作中解脫。

1. 具體成果與驗證

．產出物： 一組符合品牌規範的圖文廣告。

．驗證標準： 圖像尺寸正確、文案包含必要關鍵字、預測點擊率 (pCTR) 超過設定門檻（如 0.7）。

2. 系統基礎與功能組件

．數據與存儲： S3 (品牌圖庫)、DynamoDB (任務狀態)。

．執行功能 (Functions)： AWS Lambda (圖片合成、Meta API 串接)。

．預測能力： SageMaker 部署的評分模型。

．生成能力： Amazon Bedrock (Claude) 負責文字與提示詞生成。

3. 業務流程設計 (流程設計師視角)

．【觸發與規劃】： S3 接收到新產品資料夾，Agent 大腦啟動，將任務拆解為「分析產品 -> 生成文案 -> 合成圖片 -> 執行品質檢查」。

．【上下文裝配】： 從 Vector DB 撈取該品牌過去最受歡迎的貼文風格，從 S3 撈取正確的 Logo 與產品色號。

．【多步執行】： Agent 先調用 Lambda 合成圖片，再調用 Bedrock 生成匹配文案。如果品質檢查 Agent (由小模型擔任) 判定圖片背景太雜亂，則發回重做。

．【成果交付】： 完成最終 Payload，推送到 Meta 廣告後台排程。

4. 閉環演進 (學習路徑)

．評估： 廣告上線三天後，從 Meta API 回傳真實點擊數據。

．回饋與調整： Agent 讀取真實數據，與當初預測的 pCTR 進行比對。

．Fine-Tuning： 將「高點擊、高品質」的案例轉為訓練集，透過 Bedrock Fine-tuning 讓模型更懂該品牌的「美感標準」。

▋ 案例二：Databricks 分析層 -「分店成效自動診斷 Agent」

這個 Agent 的定位是「數據中心的診斷專家」，目標是從海量數據中主動抓出問題並給出指令。

1. 具體成果與驗證

．產出物： 包含「異常原因」與「排程修正指令」的 JSON 文件。

．驗證標準： 診斷結果與實際數據相符（如：指出 A 店銷量跌是因為人流降），且建議指令能被 CMS 系統正確執行。

2. 系統基礎與功能組件

．數據基石： Delta Lake 金級表 (零售、人流、播放紀錄)。

．工具箱 (Tools)： Unity Catalog 定義的 SQL Function (具備數據讀取權限)。

．分析能力： MLflow 管理的 Uplift 歸因模型。

．核心大腦： Mosaic AI 託管的大型語言模型。

3. 業務流程設計 (流程設計師視告)

．【觸發與規劃】： 每日 DLT 數據更新完畢後，Agent 啟動。規劃任務為：「篩選 ROI 異常店點 -> 交叉比對環境變數 -> 生成預算搬移建議」。

．【上下文裝配】： 撈取「分店主檔」了解該店商圈屬性。撈取 SQL Function 獲取前 24 小時的各店播放 Log 與銷售額。

．【多步執行】： Agent 撰寫 SQL 並執行。若發現 A 店數據奇怪，它會「主動」再執行一條 SQL 查詢該店設備是否有離線紀錄，進行深度探查。

．【成果交付】： 產生診斷報告與優化指令，發送到管理者 Slack 頻道。

4. 閉環演進 (學習路徑)

．評估： 使用「模型評估模型 (LLM-as-a-judge)」來評斷 Agent 診斷邏輯是否嚴謹。

．回饋與調整： 管理者在 Slack 點擊「同意、忽略、或修正建議」。

．Fine-Tuning： 被管理者修正過的決策會存入 Delta Lake。當案例累積足夠，透過 Mosaic AI 進行模型蒸餾 (Distillation)，將專家決策行為內化進較低成本的小模型。

▋ 開發者應掌握的「Agent 核心邏輯」

要將功能串成 Agent，同仁在開發時應關注以下三個關鍵點：

1. 從「程式邏輯」轉向「工具契約」

不要寫死所有的 if-else。

開發者的職責是寫好一個個功能強大且穩定的 Function（定義清楚輸入/輸出），

並將這些「工具」交給 Agent。

Agent 的工作是根據當前狀況，決定「現在該拿哪一把工具」。

2. 狀態管理與編排 (Orchestration)

Agent 的流程通常是循環的。

例如在分析數據時，如果發現結果不合理，

Agent 必須能「回到上一步」重新撈資料。

這需要使用 LangGraph (Databricks 推薦) 或 Step Functions (AWS 推薦) ，

來管理這些複雜的跳轉狀態。

3. 上下文工程 (Context Engineering)

Agent 的智慧來自於你給它什麼資訊。

．短期記憶： 這兩分鐘內我們聊了什麼、做了哪些 SQL。

．長期記憶： 儲存在 Vector DB 裡的業務規範、歷史報表與成功案例。 

開發者需要設計精準的檢索機制，確保 Agent 在做決定時，

手邊拿到的都是「正確且最新」的參考資料。

▋實務重點、技巧與陷阱

Scoping (定義邊界)：

．不要試圖一次自動化整個客服流程。

先切出一個「邊界清晰」的任務（如取消未發貨訂單）。

．Hybrid Strategy (混合策略)：

複雜問題交給 GPT-4o，簡單例行公事交給便宜的小模型，

優化成本與延遲。

．Human-in-the-loop (人工介入)：

在高風險決策（如退款金額過大）時，設計機制讓 Agent 暫停

並請求人工審核。

陷阱 (Traps)：

．過度編排 (Over-Orchestration)，

建立過於複雜的多 Agent 系統，導致 Token 消耗劇增且難以調試。

．GPU 資源瓶頸：忽略了模型推理的延遲與併發限制，

未設計異步 (Asynchronous) 處理機制。

．未測試的 Agent 是不可信的：隨機性是 LLM 的天性。

如果沒有建構自動化評估腳本（Evaluation script），系統上線後會是災難。

．記憶膨脹：

未經管理的長期記憶會導致檢索到不相關的資訊，干擾大腦判斷。

▋實戰踩坑：從業界經驗學習

重要認知：

Vibe Coding 讓「寫程式」變簡單，

但這不等於「做出能上線的 Agent 產品」也變簡單。

Agent 的難點不是 code，

而是進 production 會失敗（95% 的失敗率）。

失敗主因通常不是模型不夠聰明，

而是周邊工程：

context / memory / error handling / RAG / evals / feedback loop / 成本與路由。

而且模型與 best practice 更新超快：幾個月就可能要換模型、重想整套框架。

Flask 作者 Armin：實戰踩坑的工程觀察：

SDK 選擇方面，

高階抽象（如統一 SDK）看似美好，但模型差異太大；

最後更傾向用 Anthropic/OpenAI 原生 SDK，自己建立抽象層。

快取（cache）顯式 cache points 一開始很蠢，

後來發現能讓成本/命中率更可預測，

也支援 context 編輯、對話分支。

Reinforcement 增強回饋：

工具執行完不只回資料，還要塞「目標/狀態/提示」進去，

對穩定性很關鍵。

錯誤處理可用子 agent 跑到成功再回報；

同時要讓 agent 知道「哪些方法試過沒用」避免重踩坑。

共享狀態需要共用資料區（他們用虛擬檔案系統）避免工具與子 agent 資料孤島。Testing/Evals 最難：

傳統測試不太適用，仍缺滿意解法。

反思 MCP：很多 MCP server 過度設計吃 context；

有時簡單 CLI + bash 更好。

為什麼 95% production 失敗：其實在做 context selection 系統：

多數團隊以為在做 AI，其實在做上下文選擇（context selection）。

Context Engineering ≠ prompt 技巧：

很多時候 RAG 做好就夠，fine-tuning 未必必要；

但 RAG 常做得太天真。

Context 工程更像「給 LLM 做特徵工程」：

裁剪、驗證、可觀測性都是硬功。

Text-to-SQL 很殘酷：語意歧義 + 商業術語定義不同；

成功團隊會做詞彙表、查詢模板、驗證層、回饋迴圈。

信任是人的問題：成功的 5% 通常是人機協作（AI 當助手而非自主決策）+ 迭代式回饋。

記憶是架構決策：要分個人/團隊/組織；

還牽涉隱私界線。

多模型調度：用模型路由平衡成本/延遲/難度，而且路由策略本身要能學習優化。

Surge AI：Agent 能力金字塔與失敗模式：

即便頂級模型，在模擬職場任務仍大量失敗（>40%）。

能力層級（由低到高）包括：

工具使用與規劃（拆步驟、選工具、對參數、按步執行不跑偏）、

適應力（遇到錯誤/找不到要會改策略，像人一樣換查法）、

接地能力（不亂編 ID/事實、不脫離系統脈絡）、

常識推理（能做合理判斷，如退貨 vs 取消、先縮小搜尋空間等）。

結論氛圍：

2025 不是「通用 agent 已成」，而是「終於能穩定行動，開始正面檢驗常識推理」。

解方方向：Agent 產品應該更有主見（Opinionated）：

彈性是陷阱，用戶不想調溫度/分塊策略，他們想要「結果」。

產品應替用戶做前置決策：

用你的真實場景測模型（別只信 benchmark）、

prompt 清楚定義「成功長怎樣、怎麼達成」、

每個必填選項都代表你沒替用戶做決定。

模型不是可隨意替換的零件：

框架設計會綁定模型強弱點；升級模型常會打壞框架。

從深且窄開始：

先做能產生最大價值的 10% 任務，窄到能徹底優化、深到值得投資。

例子：

Anthropic 走向「領域 + 框架優化」（prompt/tool/context/sub-agent），

Claude Code/Codex 也都內建很多決策。