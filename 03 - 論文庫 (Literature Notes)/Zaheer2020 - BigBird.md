---
title: "Big Bird: Transformers for Longer Sequences"
authors: ["Manzil Zaheer", "Guru Guruganesh", "Kumar Avinash Gautam", "Arash Ainslie", "Sanjeev Arora", "et al."]
year: 2020
venue: "NeurIPS 2020"
arxiv: "2007.14062"
url: "https://arxiv.org/abs/2007.14062"
pdf_file: "Papers/01 - Long Context & Sequence/(NeurIPS 2020-12) Big Bird - Transformers for Longer Sequences.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
tags:
  - paper
  - sparse-attention---graph-theoretical-attention
---

# Big Bird: Transformers for Longer Sequences

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Manzil Zaheer, Guru Guruganesh, Kumar Avinash Gautam, Arash Ainslie, Sanjeev Arora, et al.
> - **年份 / 會議**：2020 (NeurIPS 2020)
> - **arXiv**：[2007.14062](https://arxiv.org/abs/2007.14062)
> - **論文分類**：`Sparse Attention / Graph Theoretical Attention`
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(NeurIPS 2020-12) Big Bird - Transformers for Longer Sequences.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**從圖論角度證明稀疏注意力的圖連通性，結合隨機注意力、局部窗口與全域節點，兼具理論圖性質與線性複雜度。**

---

## 核心痛點與研究背景 (Problem Statement)
簡單的局部稀疏注意力無法保證序列兩端節點之間的訊息流動效率，缺乏嚴謹的理論近似保證。

---

## 核心方法與技術架構 (Methodology & Architecture)
將注意力矩陣視為有向圖，證明只要注意力圖具備低直徑與快速混合特性即可保留全注意力的表達力。BigBird 包含三個部分：$g$ 個全域 token、$w$ 個局部窗口 token、以及 $r$ 個均勻隨機採樣 token，圖直徑大幅縮減至常數級別。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Sparse Attention / Graph Theoretical Attention 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：在理論上保證了圖連通性與 Turing 完備性，長序列問答與摘要效果優於純滑動窗口；缺點：隨機稀疏樣式的 GPU 記憶體存取非連續，硬體實作效率低於硬體優化後的稠密計算（如 FlashAttention）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
促使學界反思『純架構稀疏』與『硬體感知稠密』之間的競爭，確立了稀疏圖結構在長序列建模中的理論極限。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
