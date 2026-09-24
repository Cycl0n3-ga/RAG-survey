---
title: "Dense Passage Retrieval for Open-Domain Question Answering"
authors: ["Vladimir Karpukhin", "Barlas Oğuz", "Sewon Min", "Patrick Lewis", "Ledell Wu", "Sergey Edunov", "Danqi Chen", "Wen-tau Yih"]
year: 2020
venue: "EMNLP 2020"
arxiv: "2004.04906"
url: "https://arxiv.org/abs/2004.04906"
pdf_file: "Papers/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
tags:
  - paper
  - dense-dual-encoder-retrieval
---

# Dense Passage Retrieval for Open-Domain Question Answering

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Vladimir Karpukhin, Barlas Oğuz, Sewon Min, Patrick Lewis, Ledell Wu, Sergey Edunov, Danqi Chen, Wen-tau Yih
> - **年份 / 會議**：2020 (EMNLP 2020)
> - **arXiv**：[2004.04906](https://arxiv.org/abs/2004.04906)
> - **論文分類**：`Dense Dual-Encoder Retrieval`
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**以雙塔 BERT 結構取代傳統 BM25 關鍵字檢索，奠定向量資料庫語意搜尋的黃金標準。**

---

## 核心痛點與研究背景 (Problem Statement)
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

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：語意泛化強、離線預算 Passage 向量後線上可用 FAISS 做亞毫秒級 ANN 檢索；缺點：雙塔在單一向量中過度壓縮整個段落，容易遺失專有名詞、代號與極細微數字細節。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開啟了向量數據庫（Vector DB）與神經語意檢索時代，為所有現代 RAG 系統提供標準向量檢索基底。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
