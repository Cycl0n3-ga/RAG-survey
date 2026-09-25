---
paper_id: "Li2024_SnapKV"
title: "SnapKV: LLM Knows What You are Looking for Before Generation"
authors:
  - "Yuhong Li"
  - "Yingbing Huang"
  - "Bowen Yang"
  - "Bolei Ma"
  - "Chenghao Cui"
  - "et al."
year: 2024
publication_year: 2024
venue: "NeurIPS 2024"
doi: null
arxiv: "2404.14469"
url: "https://arxiv.org/abs/2404.14469"
pdf_file: "Papers/02 - Compression & KV Cache/(arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation.pdf"
tags:
  - "paper"
  - "kv-cache-pruning"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "A02"
primary_domain: null
secondary_domains:
  - "D14"
paradigm_tags:
  - "kv_cache"
  - "inference_efficiency"
adjacent_interfaces:
  - "A02"

---

# SnapKV: LLM Knows What You are Looking for Before Generation

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Li2024_SnapKV`
> - **作者**：Yuhong Li, Yingbing Huang, Bowen Yang, Bolei Ma, Chenghao Cui, et al.
> - **預印本初次發布年份 (Preprint)**：2024
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (NeurIPS 2024)
> - **DOI**：無
> - **arXiv**：[2404.14469](https://arxiv.org/abs/2404.14469)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**利用 Prompt 末端觀察窗口的注意力分佈，在 Prefill 階段精準挑選核心 KV 特徵，剪掉 80% 以上的歷史快取。**

---

## 研究背景與問題定義 (Problem Statement)
長文本在 Prefill 之後，KV Cache 隨長度呈線性增長，然而大部分歷史 token 在生成過程中極少被再次關注（注意力稀疏性）。

---

## 核心方法與技術架構 (Methodology & Architecture)
發現 LLM 在 Prefill 階段的末尾幾個 token（Observation Window）會自發對全文進行全域檢索，其注意力特徵能高度預測後續生成所需的重要歷史區塊。SnapKV 藉此挑選出每一層、每個 Attention Head 最重要的局部特徵聚類並永久保留，其餘 KV 直接丟棄。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["KV Cache Pruning 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 (Page 6): 在 16k 與 32k 長度的 LongBench 評測中，僅保留 20% 的 KV 快取即可達到與 Full Cache 99.4% 的綜合準確率吻合度，Prefill 後解碼速度提升 3.2x。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：生成階段顯存恆定、推論吞吐量提升 3-4x；缺點：如果後續多輪對話中提問轉移了主題，先前被丟棄的 KV Cache 無法找回，必須重新 Prefill。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開啟了『動態注意力引導的 KV 快取剪枝』新方向，是現代長文邊緣推論與高併發伺服器的重要核心組件。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A02 Context/KV Compression & Inference Efficiency]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
