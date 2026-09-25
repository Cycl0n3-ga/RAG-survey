---
paper_id: "Bai2024_LongBench"
title: "LongBench: A Bilingual, Multitask Benchmark for Long Context Understanding"
authors:
  - "Yushi Bai"
  - "Xin Lv"
  - "Jiajie Zhang"
  - "Hongchang Lyu"
  - "Jiankai Tang"
  - "Zihan Wang"
  - "et al."
year: 2023
publication_year: 2024
venue: "ACL 2024"
doi: null
arxiv: "2308.14508"
url: "https://arxiv.org/abs/2308.14508"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) LongBench - A Bilingual, Multitask Benchmark for Long Context Understanding.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - "paper"
  - "comprehensive-long-context-benchmark"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "A01"
primary_domain: null
secondary_domains:
  - "D13"
paradigm_tags:
  - "long_context_evaluation"
adjacent_interfaces:
  - "A01"

---

# LongBench: A Bilingual, Multitask Benchmark for Long Context Understanding

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Bai2024_LongBench`
> - **作者**：Yushi Bai, Xin Lv, Jiajie Zhang, Hongchang Lyu, Jiankai Tang, Zihan Wang, et al.
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ACL 2024)
> - **DOI**：無
> - **arXiv**：[2308.14508](https://arxiv.org/abs/2308.14508)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) LongBench - A Bilingual, Multitask Benchmark for Long Context Understanding.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**清華大學提出首個雙語、多任務、長序列綜合評測基準，涵蓋單篇問答、多篇問答、摘要、少樣本學習等 21 個子任務。**

---

## 研究背景與問題定義 (Problem Statement)
早期評測主要依賴單一的合成任務（如 Passkey Retrieval），無法真實反映模型在複雜現實長文本任務（如合約分析、論文總結）中的綜合理解力。

---

## 核心方法與技術架構 (Methodology & Architecture)
構建涵蓋中英文的長文本數據集，平均長度在 5k 至 16k tokens 之間。劃分為六大核心能力維度：單文檔 QA、多文檔 QA、長文摘要、Few-shot 學習、合成代碼/鍵值檢索、代碼調試。提出全自動化的評估協議。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Comprehensive Long-Context Benchmark 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 (Page 6): 評估 14 個主流大模型在 21 個長文子任務上的綜合表現；揭露許多宣稱支援 16k 的模型在真實長文任務上的分數不及 2-shot 检索基線。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：任務多樣、真實性高、雙語覆蓋全面，成為評估長文本模型綜合實力的行業標準；缺點：平均長度上限約 32k，隨著 2024 年 100k+ 時代到來需要更高維度基準補充。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
成為評估 LLM 長文本能力最權威的公認指標之一，被幾乎所有長文本模型論文引用評測。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
