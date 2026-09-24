---
paper_id: "Jiang2023_LLMLingua"
title: "LLMLingua: Compressing Context for Accelerated Inference of Large Language Models"
authors:
  - "Huiqiang Jiang"
  - "Qianhui Wu"
  - "Chin-Yew Lin"
  - "Yuqing Yang"
  - "Lili Qiu"
year: 2023
publication_year: 2023
venue: "EMNLP 2023"
doi: null
arxiv: "2310.05736"
url: "https://arxiv.org/abs/2310.05736"
pdf_file: "Papers/02 - Compression & KV Cache/(EMNLP 2023-12) LLMLingua - Compressing Context for Accelerated Inference of Large Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]"
tags:
  - "paper"
  - "prompt-token-pruning"
verification_status: "verified"
last_verified: "2026-09-24"
---

# LLMLingua: Compressing Context for Accelerated Inference of Large Language Models

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Jiang2023_LLMLingua`
> - **作者**：Huiqiang Jiang, Qianhui Wu, Chin-Yew Lin, Yuqing Yang, Lili Qiu
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2023 (EMNLP 2023)
> - **DOI**：無
> - **arXiv**：[2310.05736](https://arxiv.org/abs/2310.05736)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(EMNLP 2023-12) LLMLingua - Compressing Context for Accelerated Inference of Large Language Models.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**使用小型語言模型計算資訊熵，粗細粒度動態刪除冗餘 Token，達成高達 20x 的 Prompt 壓縮。**

---

## 研究背景與問題定義 (Problem Statement)
長文本 Prompt 造成推論延遲極長、API 成本高昂，且許多 prompt 包含大量語法輔助詞與低資訊量冗餘文本。

---

## 核心方法與技術架構 (Methodology & Architecture)
利用小型語言模型（如 LLaMA-7B 或 GPT-2）評估每個 token 的條件困惑度（Perplexity）。提出：1. Budget Controller：在組件、句子、Token 三層級分配保留預算；2. Iterative Token Compression：動態剪枝高熵/低資訊 token。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Prompt Token Pruning 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 (Page 6): 在 GSM8K 與 BBH 基準上實現高達 20x 的 Prompt 壓縮比，同時保留 98% 以上的原始模型生成品質，端到端推論延遲降低達 3.9x。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：黑盒子通用（無需修改下游 LLM 權重）、大幅降低推論延遲與成本；缺點：屬於非語義重寫的強制刪字，容易破壞關鍵的條件修飾詞、數字、實體名稱。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
Prompt 壓縮領域的標誌性架構，確立了『以小模型為先驗進行前置 Token 剪枝』的研究範式。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
