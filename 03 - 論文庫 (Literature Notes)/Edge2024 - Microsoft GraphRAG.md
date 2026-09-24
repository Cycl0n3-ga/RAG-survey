---
title: "From Local to Global: A Graph RAG Approach to Query-Focused Summarization"
authors: ["Darren Edge", "Ha Trinh", "Newman Cheng", "Joshua Bradley", "Alex Chao", "Apurva Mody", "Steven Truitt", "Jonathan Larson"]
year: 2024
venue: "Microsoft Research / arXiv 2024"
arxiv: "2404.16130"
url: "https://arxiv.org/abs/2404.16130"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]"
tags:
  - paper
  - graph-rag---global-sensemaking
---

# From Local to Global: A Graph RAG Approach to Query-Focused Summarization

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Darren Edge, Ha Trinh, Newman Cheng, Joshua Bradley, Alex Chao, Apurva Mody, Steven Truitt, Jonathan Larson
> - **年份 / 會議**：2024 (Microsoft Research / arXiv 2024)
> - **arXiv**：[2404.16130](https://arxiv.org/abs/2404.16130)
> - **論文分類**：`Graph RAG / Global Sensemaking`
> - **本地 PDF 連結**：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**微軟提出的 GraphRAG 框架，透過實體抽取、圖社群檢測（Leiden）與分層摘要，解決整體性宏觀問題（Global Sensemaking）。**

---

## 核心痛點與研究背景 (Problem Statement)
標準 Vector RAG 面臨『局部事實檢索強，全域宏觀理解弱』的致命缺陷。對於『整份文件集討論的核心主題是什麼？』等全域性問題，Top-K 向量檢索完全失效。

---

## 核心方法與技術架構 (Methodology & Architecture)
1. Extract：利用 LLM 從長文本中提取實體（Entities）、關係（Relationships）與主張（Claims）；2. Graph Clustering：使用 Leiden 社群檢測演算法將知識圖譜劃分為多層次社群（Communities）；3. Community Summaries：自底向上為每個社群生成預先摘要；4. Global Search：以 Map-Reduce 方式平行檢索社群摘要並彙整最終答案。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Graph RAG / Global Sensemaking 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：全域主題理解能力、跨實體關係推理能力遠超傳統 RAG；缺點：建索引過程需要極大量的 LLM API 呼叫，索引成本高達傳統 RAG 的數十倍。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
2024 年長文知識庫領域最具震撼力的突破之一，確立了圖結構在整體語料庫理解中的統治地位。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
