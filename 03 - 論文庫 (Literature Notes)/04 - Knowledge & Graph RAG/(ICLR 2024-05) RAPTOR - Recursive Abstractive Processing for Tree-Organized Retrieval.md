---
paper_id: "Sarthi2024_RAPTOR"
title: "RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval"
authors:
  - "Parth Sarthi"
  - "Salman Abdullah"
  - "Aditi Tuli"
  - "Shubh Khanna"
  - "Anna Goldie"
  - "Christopher D. Manning"
year: 2024
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2401.18059"
url: "https://arxiv.org/abs/2401.18059"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval.pdf"
tags:
  - "paper"
  - "recursive-summary-tree"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "D04"
primary_domain: "D04"
secondary_domains:
  - "D05"
paradigm_tags:
  - "hierarchical_rag"
  - "multi_resolution"
adjacent_interfaces: []

---

# RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Sarthi2024_RAPTOR`
> - **作者**：Parth Sarthi, Salman Abdullah, Aditi Tuli, Shubh Khanna, Anna Goldie, Christopher D. Manning
> - **預印本初次發布年份 (Preprint)**：2024
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ICLR 2024)
> - **DOI**：無
> - **arXiv**：[2401.18059](https://arxiv.org/abs/2401.18059)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**史丹佛大學提出 RAPTOR，藉由遞迴分群與摘要構建樹狀索引，同時兼顧局部細節與高階全域語義檢索。**

---

## 研究背景與問題定義 (Problem Statement)
長篇書籍、超長論文包含不同層次的語義結構（段落、章節、全書主題），扁平的 Chunking 只能檢索局部碎片，無法回答橫跨全書的宏觀問題。

---

## 核心方法與技術架構 (Methodology & Architecture)
RAPTOR（Recursive Abstractive Processing for Tree-Organized Retrieval）構建了一種遞迴抽象分層樹狀索引結構，核心流程分為建樹與檢索兩大階段：
1. **遞迴分群與抽象摘要（Recursive Clustering & Summarization）**：
   - 文本切塊與嵌入：將長文切分成固定長度（如 100 tokens）的葉節點（Leaf Chunks）並計算密集向量；
   - 降維與軟分群：使用 UMAP 進行非線性降維，再利用高斯混合模型（Gaussian Mixture Model, GMM）進行**軟分群（Soft Clustering）**——允許單一節點依機率隸屬於多個語意分群；**分群依據是向量空間中的語義鄰近度，而非文本在原文中的物理線性相鄰**；
   - 抽象摘要：呼叫 LLM 為每個分群撰寫高度概括的摘要，作為上一層的父節點；
   - 遞迴重複：對生成的摘要節點再次執行嵌入、UMAP 降維、GMM 分群與摘要，直至收斂至頂層根節點。
2. **檢索模式（Retrieval Modes）**：
   - **樹狀遍歷（Tree Traversal）**：由根節點出發，依向量相似度逐層向下貪婪擴展剪枝；
   - **全層坍縮檢索（Collapsed Tree Retrieval）**：將所有層級的原始葉節點與各層摘要節點扁平化放入同一個向量池中統一比對，使檢索器能同時捕捉高階宏觀論述與底層細粒度事實。
3. **重要學術邊界**：
   - RAPTOR 是一種**文件分層索引與檢索架構（Hierarchical Indexing & Retrieval）**；
   - **嚴禁將其與推論期的 Tree-of-Thought（ToT）推理搜尋混淆**：ToT 是在生成時對思考鏈進行分叉、評估與回溯的解碼策略，而 RAPTOR 是在檢索前構建文件語意的多分辨率摘要樹。

```mermaid
flowchart TD
    subgraph indexing["離線遞迴建樹 (Recursive Tree Construction)"]
        L["原始文本葉節點 (Leaf Chunks)"] --> EMB["計算 Text Embeddings"]
        EMB --> UMAP["UMAP 降維 + GMM 軟分群<br/>(基於語義相似度，非原文相鄰)"]
        UMAP --> LLM_SUM["LLM 抽象摘要生成"]
        LLM_SUM --> L1["Level 1 抽象摘要節點"]
        L1 --> REC["遞迴聚類與摘要"]
        REC --> L2["Level 2 / Root 宏觀摘要節點"]
    end

    subgraph retrieval["線上檢索 (Collapsed Tree Retrieval)"]
        Q["使用者問題 Query"] --> POOL["全層坍縮檢索池<br/>{Leafs + Level 1 + Level 2}"]
        POOL --> COS["向量相似度篩選 Top-k 節點<br/>(兼具宏觀摘要與微觀細節)"]
        COS --> GEN["下游 LLM 循證回答"]
    end
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 & Table 2 (Page 6-7): 在 QuALITY 超長小說選擇題數據集上，RAPTOR 結合 UnifiedQA-3B 達到 82.6% 準確率 (超越 SOTA 基線達 4.0 個百分點)；在 NarrativeQA 與 QASPER 上亦全面優於標準 DPR 與 BM25，證明全層坍縮樹狀檢索在超長文本宏觀整合問答上之實證優勢。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢**：打破了傳統 Chunking 只能檢索局部碎片的死穴，能夠在單一檢索池中同時調度全書主題背景與精確細節。
- **限制**：建樹成本高昂（需對各層次分群呼叫大量 LLM 摘要 API）；若底層摘要產生幻覺或關鍵資訊漏失，上層父節點會永久繼承並放大該偏差（誤差層級傳播）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
長文件階層式檢索（Hierarchical Indexing）的奠基之作，啟發了後續包括 Microsoft GraphRAG 在內的階層式感知與多解析度檢索設計。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 04 - Knowledge Representation & Indexing|D04 Knowledge Representation & Indexing]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
