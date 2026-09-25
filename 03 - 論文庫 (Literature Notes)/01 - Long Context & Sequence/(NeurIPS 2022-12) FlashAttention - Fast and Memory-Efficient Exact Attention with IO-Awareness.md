---
paper_id: "Dao2022_FlashAttention"
title: "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness"
authors:
  - "Tri Dao"
  - "Daniel Y. Fu"
  - "Stefano Ermon"
  - "Atri Rudra"
  - "Christopher Ré"
year: 2022
publication_year: 2022
venue: "NeurIPS 2022"
doi: null
arxiv: "2205.14135"
url: "https://arxiv.org/abs/2205.14135"
pdf_file: "Papers/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness.pdf"
tags:
  - "paper"
  - "hardware-io-aware-exact-attention"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "A01"
primary_domain: null
secondary_domains: []
paradigm_tags:
  - "long_context"
adjacent_interfaces:
  - "A01"

---

# FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Dao2022_FlashAttention`
> - **作者**：Tri Dao, Daniel Y. Fu, Stefano Ermon, Atri Rudra, Christopher Ré
> - **預印本初次發布年份 (Preprint)**：2022
> - **正式發表年份 / 會議或期刊 (Venue)**：2022 (NeurIPS 2022)
> - **DOI**：無
> - **arXiv**：[2205.14135](https://arxiv.org/abs/2205.14135)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**從 GPU 記憶體階層（SRAM vs HBM）出發重構 Attention 計算，不犧牲任何精確度實現 2-4x 加速與顯存線性節省。**

---

## 研究背景與問題定義 (Problem Statement)
標準 Attention 運算中瓶頸不在於 FLOPs，而在於 GPU 高頻寬記憶體（HBM）與晶上靜態隨機存取記憶體（SRAM）之間的反覆資料讀寫（Memory Bound），且儲存 $N \times N$ 注意力矩陣佔用巨量顯存。

---

## 核心方法與技術架構 (Methodology & Architecture)
利用 Tiling 技術將 $Q, K, V$ 分塊載入 SRAM，並使用 Online Softmax（藉由動態累計正規化常數與最大值）在局部完成計算，完全不向 HBM 寫入龐大的 $N \times N$ 中間注意力矩陣；在反向傳播時透過 SRAM 重新計算而非快取中間值。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Hardware IO-Aware Exact Attention 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 (Page 6): BERT-large 訓練速度提升 15%，GPT-2 (1k 序列) 加速 3x；Figure 2 (Page 4): SRAM Tiling 與 Online Softmax 消除 HBM 記憶體訪問瓶頸；在 64k 序列長度下無 OOM 崩潰。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：完全精確（Exact Attention）、無精度損失、顯存佔用從 $O(L^2)$ 降為 $O(L)$；缺點：運算複雜度本質仍為二次方，對百萬級別極限長度仍需搭配分散式或架構革新。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
奠定了現代長文本 LLM（如 LLaMA、Mistral、GPT-4）能夠將原生 Context 擴展至 32k/128k 甚至更長工程實現的底層基石。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A01 Long Context & Sequence Architecture]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
