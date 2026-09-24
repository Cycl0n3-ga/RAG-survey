---
title: "Longformer: The Long-Document Transformer"
authors: ["Iz Beltagy", "Matthew E. Peters", "Arman Cohan"]
year: 2020
venue: "arXiv / ACL 2020"
arxiv: "2004.05150"
url: "https://arxiv.org/abs/2004.05150"
pdf_file: "Papers/01 - Long Context & Sequence/(ACL 2020-07) Longformer - The Long-Document Transformer.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
tags:
  - paper
  - sparse-attention
---

# Longformer: The Long-Document Transformer

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Iz Beltagy, Matthew E. Peters, Arman Cohan
> - **年份 / 會議**：2020 (arXiv / ACL 2020)
> - **arXiv**：[2004.05150](https://arxiv.org/abs/2004.05150)
> - **論文分類**：`Sparse Attention`
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(ACL 2020-07) Longformer - The Long-Document Transformer.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**提出結合局部滑動窗口注意力、擴張窗口與全域特定 token 注意力的稀疏注意力機制，使長度複雜度降為線性 $O(L)$。**

---

## 核心痛點與研究背景 (Problem Statement)
標準 Transformer 的 $O(L^2)$ 複雜度使得處理數萬 token 的長文件（如學術論文、法律案件）在當時硬體上幾乎不可能。

---

## 核心方法與技術架構 (Methodology & Architecture)
設計階層稀疏注意力模式：1. Sliding Window Attention（局部周圍 token 交互）；2. Dilated Sliding Window（跳躍窗口擴大感受野）；3. Global Attention（在特定預設 token 如 [CLS] 或問題 token 上開放全域雙向注意力）。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Sparse Attention 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：計算與顯存複雜度嚴格隨序列長度呈線性增長；缺點：非預設 global token 之間的遠距離信息傳遞需要跨越多個層次，對於複雜的多跳推理（Multi-hop reasoning）容易漏掉弱相關但關鍵的證據。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
早期長文本處理的核心代表作，啟發了後續 BigBird 以及現代 KV Cache 稀疏選取（如 SnapKV）的拓撲思考。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
