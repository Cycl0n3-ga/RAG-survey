---
paper_id: "Ding2024_LongRoPE"
title: "LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens"
authors:
  - "Yiran Ding"
  - "Li Lyna Zhang"
  - "Chengruidong Zhang"
  - "Yuanyuan Xu"
  - "Ning Shang"
  - "Jiahang Xu"
  - "Fan Yang"
  - "Mao Yang"
year: 2024
publication_year: 2024
venue: "ICML 2024"
doi: null
arxiv: "2402.13753"
url: "https://arxiv.org/abs/2402.13753"
pdf_file: "Papers/01 - Long Context & Sequence/(ICML 2024-07) LongRoPE - Extending LLM Context Window Beyond 2 Million Tokens.pdf"
tags:
  - "paper"
  - "positional-encoding-extension"
verification_status: "verified"
last_verified: "2026-09-24"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "A01"
primary_domain: null
secondary_domains: []
paradigm_tags:
  - "long_context"
adjacent_interfaces:
  - "A01"

---

# LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Ding2024_LongRoPE`
> - **作者**：Yiran Ding, Li Lyna Zhang, Chengruidong Zhang, Yuanyuan Xu, Ning Shang, Jiahang Xu, Fan Yang, Mao Yang
> - **預印本初次發布年份 (Preprint)**：2024
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ICML 2024)
> - **DOI**：無
> - **arXiv**：[2402.13753](https://arxiv.org/abs/2402.13753)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/01 - Long Context & Sequence/(ICML 2024-07) LongRoPE - Extending LLM Context Window Beyond 2 Million Tokens.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**透過演化搜尋非均勻位置插值，僅需微調 1000 步即可將 LLaMA 擴展至 2.048M 上下文。**

---

## 研究背景與問題定義 (Problem Statement)
標準 RoPE 外推會導致注意力分配劇烈混亂，而傳統線性插值（PI）或 YaRN 在極限外推比例（如 8x 以上）時高頻與低頻維度的插值嚴重破壞短距離語言建模能力。

---

## 核心方法與技術架構 (Methodology & Architecture)
1. 發現 RoPE 維度之間存在極大的不均勻性，採用演化演算法搜尋最優的非均勻頻率縮放因數；2. Progressive Extension：先從 4k 插值到 256k 微調，再以此為基座外推至 2048k，並結合長短序列兼顧策略避免短期退化。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Positional Encoding Extension 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 1 & Figure 3 (Page 6-7): 將 LLaMA2-7B 與 Mistral 原生窗口成功擴展至 2048k (2M) tokens；在 2M 長度 Passkey 檢索取得 99.8% 準確率，微調僅消耗 10 億 token。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：成本極低（微調 token 量極少）、外推長度達 2M；缺點：位置編碼插值僅解決了模型『看得懂位置』，不代表模型具備在 2M 長度下不遺忘、複雜多跳邏輯推理的能力。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
極致展現了位置編碼外推的工程極限，明確劃分了『Context Window 長度』與『Long Reasoning 深度』的本質區別。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|A01 Long Context & Sequence Architecture]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]
