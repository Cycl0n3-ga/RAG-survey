---
title: "Mamba: Linear-Time Sequence Modeling with Selective State Spaces"
authors: ["Albert Gu", "Tri Dao"]
year: 2023
venue: "arXiv 2023"
arxiv: "2312.00752"
url: "https://arxiv.org/abs/2312.00752"
pdf_file: "Papers/01 - Long Context & Sequence/(arXiv 2023-12) Mamba - Linear-Time Sequence Modeling with Selective State Spaces.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
tags:
  - paper
  - state-space-models-(ssm)---alternative-architectures
---

# Mamba: Linear-Time Sequence Modeling with Selective State Spaces

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Albert Gu, Tri Dao
> - **年份 / 會議**：2023 (arXiv 2023)
> - **arXiv**：[2312.00752](https://arxiv.org/abs/2312.00752)
> - **論文分類**：`State Space Models (SSM) / Alternative Architectures`
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(arXiv 2023-12) Mamba - Linear-Time Sequence Modeling with Selective State Spaces.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**打破 Transformer 壟斷，提出具備選擇性狀態機制的 SSM（Selective SSM），實現嚴格線性推論時間 $O(L)$ 與無限制的長度外推。**

---

## 核心痛點與研究背景 (Problem Statement)
傳統 SSM 為時不變系統（LTI），無法根據輸入內容動態決定記憶與遺忘（無法做 Contextual Selection）；而 Attention 雖具備選擇能力但推論時 KV Cache 隨長度無限膨脹。

---

## 核心方法與技術架構 (Methodology & Architecture)
使 SSM 參數（$B, C, \Delta$）依據當前輸入 $x_t$ 動態變化（選擇性機制），並提出硬體感知的平行關聯掃描演算法（Parallel Associative Scan），在 SRAM 內高效完成動態隱狀態累加，無需實體儲存巨大歷史狀態。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["State Space Models (SSM) / Alternative Architectures 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：訓練高平行、推論顯存常數級 $O(1)$、序列長度線性擴展；缺點：狀態維度固定導致資訊有失真壓縮，在 Needle In A Haystack 等精確 Copy/Recall 與跨文件關聯性查詢上仍不及 Attention 直接。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
掀起 2024-2026 年非 Attention 架構研究浪潮，促使業界發展 Attention-SSM 混合模型（如 Jamba、Nemotron-H）。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
