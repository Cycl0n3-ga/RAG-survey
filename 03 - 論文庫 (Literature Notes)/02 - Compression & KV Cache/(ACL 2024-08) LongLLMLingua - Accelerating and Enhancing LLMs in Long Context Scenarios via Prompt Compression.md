---
paper_id: "Jiang2024_LongLLMLingua"
title: "LongLLMLingua: Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression"
authors:
  - "Huiqiang Jiang"
  - "Qianhui Wu"
  - "Xufang Luo"
  - "Dongsheng Li"
  - "Chin-Yew Lin"
  - "Yuqing Yang"
  - "Lili Qiu"
year: 2023
publication_year: 2024
venue: "ACL 2024"
doi: null
arxiv: "2310.06201"
url: "https://arxiv.org/abs/2310.06201"
pdf_file: "Papers/02 - Compression & KV Cache/(ACL 2024-08) LongLLMLingua - Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]"
tags:
  - "paper"
  - "query-aware-prompt-compression"
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

# LongLLMLingua: Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Jiang2024_LongLLMLingua`
> - **作者**：Huiqiang Jiang, Qianhui Wu, Xufang Luo, Dongsheng Li, Chin-Yew Lin, Yuqing Yang, Lili Qiu
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ACL 2024)
> - **DOI**：無
> - **arXiv**：[2310.06201](https://arxiv.org/abs/2310.06201)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(ACL 2024-08) LongLLMLingua - Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**解決 LLMLingua 在長文本場景中 Lost in the Middle 的問題，引入 Question-Aware 條件感知壓縮機制。**

---

## 研究背景與問題定義 (Problem Statement)
原本 LLMLingua 是 Query-Agnostic 的，會依照文本自然語言概率刪詞，導致長文件中與問題最相關的細微線索被意外刪除，且無法緩解模型對中間段落的遺忘。

---

## 核心方法與技術架構 (Methodology & Architecture)
1. 引入問題對文件條件概率 $P(Doc|Query)$ 作為重要性評估基準；2. 依照與問題關聯度重排文檔，將高相關文件置於開頭與結尾（對抗 Lost in the Middle）；3. 動態分配不同文檔的壓縮率。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Query-Aware Prompt Compression 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 & Figure 2 (Page 5-6): 在 NaturalQuestions 多文檔 QA 中，壓縮 4x 後準確率反而提升 17.1% (濾除干擾雜訊)；有效緩解中間丟失現象，API 呼叫成本降低 75%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：長文問答準確率提升顯著，壓縮 4x 甚至出現超越原始 Prompt 表現的現象（濾除干擾雜訊）；缺點：必須預先已知 Query，無法用於長篇離線預索引快取。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
明確奠定了長文本壓縮必須區分『Query-Aware（線上動態）』與『Query-Agnostic（離線靜態）』兩大路線。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
