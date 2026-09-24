---
title: "RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval"
authors: ["Parth Sarthi", "Salman Abdullah", "Aditi Tuli", "Shubham Khanna", "Anna Goldie", "Christopher D. Manning"]
year: 2024
venue: "Stanford / ICLR 2024"
arxiv: "2401.18059"
url: "https://arxiv.org/abs/2401.18059"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]"
tags:
  - paper
  - recursive-summary-tree
---

# RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Parth Sarthi, Salman Abdullah, Aditi Tuli, Shubham Khanna, Anna Goldie, Christopher D. Manning
> - **年份 / 會議**：2024 (Stanford / ICLR 2024)
> - **arXiv**：[2401.18059](https://arxiv.org/abs/2401.18059)
> - **論文分類**：`Recursive Summary Tree`
> - **本地 PDF 連結**：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**史丹佛大學提出 RAPTOR，藉由遞迴分群與摘要構建樹狀索引，同時兼顧局部細節與高階全域語義檢索。**

---

## 核心痛點與研究背景 (Problem Statement)
長篇書籍、超長論文包含不同層次的語義結構（段落、章節、全書主題），扁平的 Chunking 只能檢索局部碎片，無法回答橫跨全書的宏觀問題。

---

## 核心方法與技術架構 (Methodology & Architecture)
遞迴構建摘要樹：1. 將原始文本切塊並嵌入向量；2. 使用高斯混合模型（GMM）進行軟分群（一個塊可屬於多個群）；3. 由 LLM 為每個群生成抽象摘要；4. 遞迴對摘要再次分群摘要，直至生成頂層根節點。推論時採用樹狀遍歷（Tree Traversal）或全層塌陷（Collapsed Tree）綜合檢索。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Recursive Summary Tree 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：在 QuALITY、NarrativeQA 等超長篇小說/報告問答基準上大幅刷新 SOTA；缺點：建樹需要多輪摘要呼叫，若底層摘要產生偏差，上層節點會持續擴大該錯誤。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
長文件階層式檢索（Hierarchical Indexing）的奠基之作，廣泛被整合進先進 RAG 生態。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
