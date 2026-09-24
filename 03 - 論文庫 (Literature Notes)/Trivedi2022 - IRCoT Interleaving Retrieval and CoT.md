---
title: "Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions"
authors: ["Harsh Trivedi", "Niranjan Balasubramanian", "Tushar Khot", "Ashish Sabharwal"]
year: 2022
venue: "ACL 2023"
arxiv: "2212.10509"
url: "https://arxiv.org/abs/2212.10509"
pdf_file: "Papers/03 - RAG & Retrieval/(ACL 2023-07) Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]"
tags:
  - paper
  - multi-hop-reasoning---iterative-retrieval
---

# Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Harsh Trivedi, Niranjan Balasubramanian, Tushar Khot, Ashish Sabharwal
> - **年份 / 會議**：2022 (ACL 2023)
> - **arXiv**：[2212.10509](https://arxiv.org/abs/2212.10509)
> - **論文分類**：`Multi-Hop Reasoning / Iterative Retrieval`
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(ACL 2023-07) Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**將思維鏈（CoT）推理與檢索交替進行（Interleaving），用中間推理步驟動態指引下一輪檢索，完美解決多跳長文推理難題。**

---

## 核心痛點與研究背景 (Problem Statement)
標準 RAG 採用單次檢索（One-shot Retrieval），然而在複雜長文問題中，後續線索必須依賴前面的推理結果才能得知（如『A 公司的母公司的創辦人是誰？』）。

---

## 核心方法與技術架構 (Methodology & Architecture)
循環迭代管線：1. 根據當前 Context 與 Query 生成一步 CoT 推理句子；2. 將該推理句子作為新的檢索 Query 檢索新證據；3. 將檢索出的新段落追加進 Context；4. 重複直到推導出最終答案。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Multi-Hop Reasoning / Iterative Retrieval 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：在 HotpotQA、2WikiMultiHop 等多跳長文問答基準上大幅擊敗單次檢索；缺點：多輪 LLM 呼叫延遲較高，且如果中間某一跳檢索引入錯誤雜訊，容易發生錯誤傳播（Error Cascade）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
奠定了 Agentic RAG 與 Iterative Multi-step Retrieval 的基礎，是複雜長文件關聯推理的核心支柱。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
