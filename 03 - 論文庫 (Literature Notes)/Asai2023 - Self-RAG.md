---
title: "Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection"
authors: ["Akari Asai", "Zeqiu Wu", "Yizhong Wang", "Avirup Sil", "Hannaneh Hajishirzi"]
year: 2023
venue: "ICLR 2024"
arxiv: "2310.11511"
url: "https://arxiv.org/abs/2310.11511"
pdf_file: "Papers/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - paper
  - adaptive-rag---self-reflection
---

# Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Akari Asai, Zeqiu Wu, Yizhong Wang, Avirup Sil, Hannaneh Hajishirzi
> - **年份 / 會議**：2023 (ICLR 2024)
> - **arXiv**：[2310.11511](https://arxiv.org/abs/2310.11511)
> - **論文分類**：`Adaptive RAG / Self-Reflection`
> - **本地 PDF 連結**：[[Papers/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**透過特殊的 Reflection Tokens 訓練 LLM 自主決定何時需要檢索、評估檢索相關性，並對自身生成的忠實度進行自我批判。**

---

## 核心痛點與研究背景 (Problem Statement)
傳統 RAG 無論問題難易與自身知識庫存，盲目觸發檢索；且對檢索出的低品質文檔缺乏批判能力，容易被噪音誤導。

---

## 核心方法與技術架構 (Methodology & Architecture)
引入四種反思標記（Reflection Tokens）：1. `[Retrieve]`（是否需要檢索）；2. `[IsREL]`（文檔是否與主題相關）；3. `[IsSUP]`（生成的主張是否受到文檔支持）；4. `[IsUSE]`（生成內容是否實用）。訓練模型輸出這些標記，並在推論時利用 Beam Search 選擇最高質量路徑。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Adaptive RAG / Self-Reflection 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：動態自適應檢索、大幅降低幻覺率、顯著提高回答忠實度（Faithfulness）；缺點：需要對模型進行專門指令微調與強化學習，增加推論時解碼複雜度。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開創了『自省式檢索（Self-Reflective RAG）』範式，是現代高品質長文知識問答與反思 Agent 的核心理論來源。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
