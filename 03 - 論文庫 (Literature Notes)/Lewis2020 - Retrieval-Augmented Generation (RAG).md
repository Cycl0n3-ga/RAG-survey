---
title: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
authors: ["Patrick Lewis", "Ethan Perez", "Aleksandra Piktus", "Fabio Petroni", "Vladimir Karpukhin", "et al."]
year: 2020
venue: "NeurIPS 2020"
arxiv: "2005.11401"
url: "https://arxiv.org/abs/2005.11401"
pdf_file: "Papers/03 - RAG & Retrieval/(NeurIPS 2020-12) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
tags:
  - paper
  - foundational-rag
---

# Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, et al.
> - **年份 / 會議**：2020 (NeurIPS 2020)
> - **arXiv**：[2005.11401](https://arxiv.org/abs/2005.11401)
> - **論文分類**：`Foundational RAG`
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(NeurIPS 2020-12) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**正式確立 RAG（檢索增強生成）框架，將參數化記憶（模型權重）與非參數化記憶（外部向量庫）完美解耦。**

---

## 核心痛點與研究背景 (Problem Statement)
純預訓練語言模型將知識死記在參數量中，導致知識無法動態更新、易生幻覺，且無法處理領域內部未公開的超長專業文檔。

---

## 核心方法與技術架構 (Methodology & Architecture)
定義端到端可微分的 RAG-Sequence 與 RAG-Token 模型：透過 DPR 檢索相關文檔作為潛變量（Latent Variable），再由 Seq2Seq 生成器條件生成文本，結合二者梯度聯合微調。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Foundational RAG 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：無需把所有資料塞入模型 Context、知識可隨外部資料庫即時更新、回答具備可追溯出處；缺點：檢索依賴 Top-K 粗糙切片，對於需要全域宏觀理解的長文任務容易斷章取義。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
整個 RAG 領域的開山鼻祖，奠定了『Retrieve $\rightarrow$ Augment $\rightarrow$ Generate』的現代工程範式。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
