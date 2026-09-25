---
paper_id: "Mu2023_GistTokens"
title: "Learning to Compress Prompts with Gist Tokens"
authors:
  - "Jesse Mu"
  - "Xiang Lisa Li"
  - "Noah D. Goodman"
year: 2023
publication_year: 2023
venue: "NeurIPS 2023"
doi: null
arxiv: "2304.08467"
url: "https://arxiv.org/abs/2304.08467"
pdf_file: "Papers/02 - Compression & KV Cache/(NeurIPS 2023-12) Learning to Compress Prompts with Gist Tokens.pdf"
tags:
  - "paper"
  - "learned-representation-compression"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "A02"
primary_domain: null
secondary_domains:
  - "D07"
paradigm_tags:
  - "context_compression"
adjacent_interfaces:
  - "A02"

---

# Learning to Compress Prompts with Gist Tokens

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Mu2023_GistTokens`
> - **作者**：Jesse Mu, Xiang Lisa Li, Noah D. Goodman
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2023 (NeurIPS 2023)
> - **DOI**：無
> - **arXiv**：[2304.08467](https://arxiv.org/abs/2304.08467)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(NeurIPS 2023-12) Learning to Compress Prompts with Gist Tokens.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**在 Prompt 末端插入可學習的 Gist Token，強制模型將整段長 Context 壓縮進少數隱向量中。**

---

## 研究背景與問題定義 (Problem Statement)
現有壓縮依賴文字層面的刪除或重寫，而 Transformer 隱層維度本身具備更強大的資訊表徵潛力。

---

## 核心方法與技術架構 (Methodology & Architecture)
在預訓練模型中加入特定的 `<gist>` 標記，並修改 Attention Mask，強制後續的回答只能對 `<gist>` token 進行關注，而不能直接回溯原始 prompt 的前面 tokens。透過監督學習強迫 Gist token 吸收長 prompt 的全部語義。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Learned Representation Compression 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 (Page 6): 在 Alpaca 與 HumanEval 上將 Prompt 壓縮多達 26x，推論 FLOPs 降低 40%，且在未經微調的泛化任務上保留了 92% 的指令遵循能力。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：極致壓縮比（數百 token 壓成 1~2 個向量）、加速顯著；缺點：需修改模型訓練注意力遮罩、缺乏可解釋性，且複雜邏輯的多跳線索難以全部無失真編碼進固定向量。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
為『隱空間 Token 壓縮（Soft Token / Memory Vector）』提供了標準範式，啟發了後續虛擬記憶體與持續狀態壓縮的研究。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A02 Context/KV Compression & Inference Efficiency]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
