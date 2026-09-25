---
paper_id: "Liu2023_RingAttention"
title: "RingAttention with Blockwise Transformers for Near-Infinite Context"
authors:
  - "Hao Liu"
  - "Matei Zaharia"
  - "Pieter Abbeel"
year: 2023
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2310.01889"
url: "https://arxiv.org/abs/2310.01889"
pdf_file: "Papers/01 - Long Context & Sequence/(ICLR 2024-05) RingAttention with Blockwise Transformers for Near-Infinite Context.pdf"
tags:
  - "paper"
  - "distributed-exact-attention"
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

# RingAttention with Blockwise Transformers for Near-Infinite Context

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Liu2023_RingAttention`
> - **作者**：Hao Liu, Matei Zaharia, Pieter Abbeel
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ICLR 2024)
> - **DOI**：無
> - **arXiv**：[2310.01889](https://arxiv.org/abs/2310.01889)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(ICLR 2024-05) RingAttention with Blockwise Transformers for Near-Infinite Context.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**利用環形通訊拓撲重疊計算與記憶體傳輸，打破單機顯存限制，實現百萬至千萬級 Exact Attention。**

---

## 研究背景與問題定義 (Problem Statement)
超長序列（如數百萬 token）即使使用 FlashAttention，其 KV Cache 依然會迅速塞爆單張甚至單節點 GPU 的 VRAM。

---

## 核心方法與技術架構 (Methodology & Architecture)
將長序列切分成多個 Block 分配至各 GPU。在 GPU 環（Ring）中，每個設備一邊計算當前 Query 與本地 Key/Value 的局部 Softmax，一邊在後台透過 P2P 通訊將 Key/Value 傳送至下一個設備，形成環狀流水線，完全隱藏通訊延遲。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Distributed Exact Attention 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Figure 4 (Page 7): 實證展示在多節點 GPU 環形通訊拓撲下，成功處理高達 512k 至 1M 的序列長度，計算與通訊完全重疊，通訊開銷佔比低於 5%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：完全精確 Attention，理論上只要增加節點即可無上限擴展 Context Window（百萬至千萬 token）；缺點：高度依賴高速跨節點通訊頻寬（如 InfiniBand），在非超級電腦架構下通訊瓶頸明顯。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
支撐了 Gemini 1.5 Pro / GPT-4o 實現 1M~10M 原生上下文工程落地的核心分散式技術之一。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A01 Long Context & Sequence Architecture]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
