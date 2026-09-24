---
paper_id: "Karpukhin2020_DPR"
title: "Dense Passage Retrieval for Open-Domain Question Answering"
authors:
  - "Vladimir Karpukhin"
  - "Barlas Oğuz"
  - "Sewon Min"
  - "Patrick Lewis"
  - "Ledell Wu"
  - "Sergey Edunov"
  - "Danqi Chen"
  - "Wen-tau Yih"
year: 2020
publication_year: 2020
venue: "EMNLP 2020"
doi: null
arxiv: "2004.04906"
url: "https://arxiv.org/abs/2004.04906"
pdf_file: "Papers/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
tags:
  - "paper"
  - "dense-dual-encoder-retrieval"
verification_status: "verified"
last_verified: "2026-09-24"
---

# Dense Passage Retrieval for Open-Domain Question Answering

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Karpukhin2020_DPR`
> - **作者**：Vladimir Karpukhin, Barlas Oğuz, Sewon Min, Patrick Lewis, Ledell Wu, Sergey Edunov, Danqi Chen, Wen-tau Yih
> - **預印本初次發布年份 (Preprint)**：2020
> - **正式發表年份 / 會議或期刊 (Venue)**：2020 (EMNLP 2020)
> - **DOI**：無
> - **arXiv**：[2004.04906](https://arxiv.org/abs/2004.04906)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**以雙塔 BERT 結構取代傳統 BM25 關鍵字檢索，奠定向量資料庫語意搜尋的黃金標準。**

---

## 研究背景與問題定義 (Problem Statement)
傳統 BM25 等詞頻匹配演算法嚴重受限於同義詞替換（Vocabulary Mismatch）與語意隱式表達，無法精準捕捉長句子背後的意圖。

---

## 核心方法與技術架構 (Methodology & Architecture)
訓練兩個獨立的 BERT 編碼器：Question Encoder $E_Q(q)$ 與 Passage Encoder $E_P(p)$，利用點積計算相似度 $\text{sim}(q, p) = E_Q(q)^T E_P(p)$。透過 In-batch Negatives 與 Hard Negative Mining 進行高效率對比學習。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Dense Dual-Encoder Retrieval 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 (Page 5): 在 Top-20 檢索準確率上，DPR 達到 78.4%，大幅超越傳統強力 BM25 的 59.1% (提升近 20 個百分點)；確立向量雙塔檢索標準。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：語意泛化強、離線預算 Passage 向量後線上可用 FAISS 做亞毫秒級 ANN 檢索；缺點：雙塔在單一向量中過度壓縮整個段落，容易遺失專有名詞、代號與極細微數字細節。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開啟了向量數據庫（Vector DB）與神經語意檢索時代，為所有現代 RAG 系統提供標準向量檢索基底。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
