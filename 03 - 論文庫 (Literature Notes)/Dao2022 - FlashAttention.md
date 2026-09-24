---
title: "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness"
authors: ["Tri Dao", "Daniel Y. Fu", "Stefano Ermon", "Atri Rudra", "Christopher Ré"]
year: 2022
venue: "NeurIPS 2022"
arxiv: "2205.14135"
url: "https://arxiv.org/abs/2205.14135"
pdf_file: "Papers/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
tags:
  - paper
  - hardware-io-aware-exact-attention
---

# FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Tri Dao, Daniel Y. Fu, Stefano Ermon, Atri Rudra, Christopher Ré
> - **年份 / 會議**：2022 (NeurIPS 2022)
> - **arXiv**：[2205.14135](https://arxiv.org/abs/2205.14135)
> - **論文分類**：`Hardware IO-Aware Exact Attention`
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**從 GPU 記憶體階層（SRAM vs HBM）出發重構 Attention 計算，不犧牲任何精確度實現 2-4x 加速與顯存線性節省。**

---

## 核心痛點與研究背景 (Problem Statement)
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

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：完全精確（Exact Attention）、無精度損失、顯存佔用從 $O(L^2)$ 降為 $O(L)$；缺點：運算複雜度本質仍為二次方，對百萬級別極限長度仍需搭配分散式或架構革新。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
奠定了現代長文本 LLM（如 LLaMA、Mistral、GPT-4）能夠將原生 Context 擴展至 32k/128k 甚至更長工程實現的底層基石。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
