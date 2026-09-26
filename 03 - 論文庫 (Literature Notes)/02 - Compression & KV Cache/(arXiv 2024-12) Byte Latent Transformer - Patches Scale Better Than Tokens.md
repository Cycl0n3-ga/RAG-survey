---
paper_id: "Pagnoni2024_BLT"
title: "Byte Latent Transformer: Patches Scale Better Than Tokens"
authors:
  - "Artidoro Pagnoni"
  - "Ram Pasunuru"
  - "Pedro Rodriguez"
  - "John Nguyen"
  - "Benjamin Muller"
  - "et al."
year: 2024
publication_year: 2025
venue: "ACL 2025"
doi: "10.18653/v1/2025.acl-long.453"
arxiv: "2412.09871"
url: "https://aclanthology.org/2025.acl-long.453/"
pdf_file: "Papers/02 - Compression & KV Cache/(arXiv 2024-12) Byte Latent Transformer - Patches Scale Better Than Tokens.pdf"
tags:
  - "paper"
  - "byte-level-patching---tokenizer-free"
verification_status: "verified"
last_verified: "2026-09-26"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "A03"
primary_domain: null
secondary_domains: []
paradigm_tags: []
adjacent_interfaces:
  - "A03"

---

# Byte Latent Transformer: Patches Scale Better Than Tokens

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Pagnoni2024_BLT`
> - **作者**：Artidoro Pagnoni, Ram Pasunuru, Pedro Rodriguez, John Nguyen, Benjamin Muller, et al.
> - **預印本初次發布年份 (Preprint)**：2024
> - **正式發表年份 / 會議或期刊 (Venue)**：2025 (ACL 2025, Long Papers; Outstanding Paper)
> - **DOI**：10.18653/v1/2025.acl-long.453
> - **arXiv**：[2412.09871](https://arxiv.org/abs/2412.09871)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(arXiv 2024-12) Byte Latent Transformer - Patches Scale Better Than Tokens.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**Meta 拋棄傳統固定 Tokenizer，以動態字節斑塊（Byte Patches）實現依資訊熵自適應分配計算量的新型架構。**

---

## 研究背景與問題定義 (Problem Statement)
固定詞表 Tokenizer 存在跨語言不平等、拼寫脆弱、領域泛化差等問題，且將長文本機械化切片，無法在複雜長句中靈活分配計算資源。

---

## 核心方法與技術架構 (Methodology & Architecture)
基於原生 Byte 輸入，使用輕量熵模型檢測資訊密度變化邊界，動態將字節聚合成 Patch（Patch 尺寸隨熵動態增減）。主幹大模型僅在 Patch 隱空間上執行 Attention 計算，再由輕量解碼器還原為 Byte。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Byte-level Patching / Tokenizer-Free 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 (Page 8): 於相同推論 FLOPs 下，BLT 在英文與跨語言長文本建模中 Perplexity 顯著優於 LLaMA-3 Tokenizer 基準，且對字符隨機噪聲具備極強魯棒性。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：徹底告別 Tokenizer 偏見、高壓縮比、長文本在非結構化資料下更穩健；缺點：需要從頭預訓練全新的基座模型，無法直接套用於現有 LLaMA/GPT 架構。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
代表了 2025-2026 年底層架構從 Token 級向 Byte 級自適應長文本建模典範轉移的重要嘗試。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A01 Long Context & Sequence Architecture]]
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A02 Context/KV Compression & Inference Efficiency]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
