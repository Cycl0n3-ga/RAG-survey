---
title: "Domain 03: 先進 RAG 與檢索機制 (Advanced RAG, ColBERT, HyDE, Self-RAG)"
tags:
  - "domain/rag"
  - research-domain
---

# Domain 03: 先進 RAG 與檢索機制 (Advanced RAG, ColBERT, HyDE, Self-RAG)

> [!ABSTRACT] 核心問題意識 (Core Problem Statement)
> **當外部資料庫或文檔集達到數百萬至數億 Token 時，如何精準、低延遲地檢索出與問題最高度相關、具備充分證據性的局部脈絡，並回傳給 LLM 進行可靠生成？**

---

### 一、核心問題意識：從 Naive RAG 到 Advanced/Agentic RAG
傳統 RAG（[[Lewis2020 - Retrieval-Augmented Generation (RAG)|Lewis et al., 2020]]）採用簡單的『切塊 $\rightarrow$ 嵌入 $\rightarrow$ 向量相似度檢索 $\rightarrow$ 生成』流程，在真實長文件處理中面臨三大破綻：
1. **語意不對稱（Semantic Asymmetry）**：短 Query 與長 Passage 在向量空間分佈不一致。
2. **單向量粗暴壓縮**：[[Karpukhin2020 - Dense Passage Retrieval (DPR)|DPR]] 將數百字壓成單一 1536 維向量，丟失了專有名詞、數字、精準代號等硬匹配資訊。
3. **盲目檢索與噪音注入**：不論問題是否已知、檢索內容是否衝突，一律無差別餵入 LLM，造成上下文污染與嚴重幻覺。

---

### 二、先進檢索架構光譜

```mermaid
graph LR
    subgraph Query Pre-processing
        Q["User Query"] --> HY["[[Gao2022 - HyDE Zero-Shot Dense Retrieval|HyDE (假想文檔生成)]]"]
        Q --> CR["Query Rewrite / Decompose"]
    end

    subgraph Retrieval Engine
        HY --> DR["Dense (DPR/BGE)"]
        HY --> SP["Sparse (BM25/SPLADE)"]
        HY --> LI["[[Khattab2020 - ColBERT Late Interaction|ColBERT (Late Interaction)]]"]
    end

    subgraph Hybrid & Rerank
        DR & SP & LI --> RR["Cross-Encoder Reranker / Cohere"]
    end

    subgraph Dynamic & Adaptive Generation
        RR --> SR["[[Asai2023 - Self-RAG|Self-RAG (反思與自我批判)]]"]
        RR --> IR["[[Trivedi2022 - IRCoT Interleaving Retrieval and CoT|IRCoT (多跳交錯檢索)]]"]
    end
```

#### 1. 密集向量與稀疏檢索之爭 (Dense vs. Sparse)
- **Dense Retrieval ([[Karpukhin2020 - Dense Passage Retrieval (DPR)|DPR]])**：擅長近義詞、抽象意圖捕捉；但在產品型號、錯誤代碼、罕見人名上表現極差。
- **Hybrid Search (BM25 + Dense + RRF)**：已成為工業界標準實踐。透過倒數排名融合（Reciprocal Rank Fusion, RRF）同時兼顧字面精確與語義泛化。

#### 2. 多向量延遲交互 (Contextualized Late Interaction)
- **代表作**：[[Khattab2020 - ColBERT Late Interaction|ColBERT (SIGIR 2020)]]、ColBERTv2。
- **機制**：對 Query 與 Document 的每一個 token 分別保留嵌入向量，檢索階段計算 MaxSim 矩陣和。既保有 Cross-Encoder 級別的細粒度 token 交互，又能在離線預先構建向量索引。

#### 3. 查詢轉換與假設文檔 (Query Transformation & HyDE)
- **代表作**：[[Gao2022 - HyDE Zero-Shot Dense Retrieval|HyDE (Gao et al., 2022)]]。
- **機制**：令 LLM 根據問題先撰寫一篇包含假想答案的完整文章，利用該假想文檔的向量去檢索資料庫。由於假想文檔在長度、句式與詞彙分佈上與真實目標文檔完全同構，能大幅彌合查詢與文檔的幾何距離。

#### 4. 自適應反思與多跳檢索 (Adaptive RAG & Multi-Hop)
- **代表作**：[[Asai2023 - Self-RAG|Self-RAG (Asai et al., 2023)]]、[[Trivedi2022 - IRCoT Interleaving Retrieval and CoT|IRCoT (Trivedi et al., 2022)]]。
- **機制**：
  - **Self-RAG**：利用 `[Retrieve]`、`[IsREL]`、`[IsSUP]` 標記訓練模型自覺判斷何時檢索、驗證文檔是否相關、檢驗輸出是否獲得文檔充分支持。
  - **IRCoT**：將思維鏈（CoT）推理與檢索循環交替，將前一步的中間推論結果作為新的檢索線索，成功攻克跨多篇文檔的複雜多跳推理。

---

### 三、Anthropic Contextual Retrieval 的啟發
2024 年 Anthropic 提出了 Contextual Retrieval 工程範式：
- **痛點**：將大文件切分為 200~300 token 的 Chunk 時，後續段落失去開頭的背景主題（如『該季度的營收增長了 5%』，在 Chunk 中丟失了『哪一年哪一家公司』）。
- **解法**：在離線切塊時，呼叫 LLM 為每一個 Chunk 前置補充 50~100 token 的文檔全域情境說明（Contextual Explanation），使每個 Chunk 在向量嵌入與 BM25 索引中均自帶完備上下文，檢索失敗率降低 49% 以上。

---

## 相關導覽與文獻快速跳轉
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
- **深度研究報告**：[[01 - 深度研究報告 (Deep Research Reports)/01 - LLM 超長文件閱讀與撰寫技術全景 (完整深度報告)|技術全景深度報告]]
- **權衡分析**：[[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術成熟度與 Pareto 權衡分析]]
