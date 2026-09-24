---
title: "Lost in the Middle: How Language Models Use Long Contexts"
authors: ["Nelson F. Liu", "Kevin Lin", "John Hewitt", "Ashwin Paranjape", "Michele Bevilacqua", "Fabio Petroni", "Percy Liang"]
year: 2023
venue: "Stanford, UC Berkeley & Samaya AI / TACL 2024"
arxiv: "2307.03172"
url: "https://arxiv.org/abs/2307.03172"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - paper
  - long-context-evaluation-&-analysis
---

# Lost in the Middle: How Language Models Use Long Contexts

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
> - **年份 / 會議**：2023 (Stanford, UC Berkeley & Samaya AI / TACL 2024)
> - **arXiv**：[2307.03172](https://arxiv.org/abs/2307.03172)
> - **論文分類**：`Long Context Evaluation & Analysis`
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**揭示所有主流長文本 LLM 普遍存在的 U 型效應：模型在利用頭尾資訊時表現優異，但對位於長 Context 中間的關鍵資訊極易視而不見。**

---

## 核心痛點與研究背景 (Problem Statement)
學界與業界盲目追求擴展 Context Window，卻未經嚴格檢驗模型是否能在百萬序列的『任何位置』都同等具備穩健的檢索與推理能力。

---

## 核心方法與技術架構 (Methodology & Architecture)
設計多文檔問答（Multi-document QA）與鍵值檢索實驗，精確控制包含答案的目標文檔在整個 Context Window 中的相對位置（0% 到 100%）。橫向評估了當時最強的各類開源與閉源模型（GPT-3.5、Claude、MPT-30B 等）。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Long Context Evaluation & Analysis 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：以嚴謹的實證數據打破了『長上下文窗口 = 完美長文本理解』的迷思；缺點：該現象在 2024 年後的頂級模型（如 Gemini 1.5 Pro）中藉由訓練改進有所緩解，但在複雜推理場景下依然潛伏存在。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
震撼整個 NLP 界，催生了後續 Needle In A Haystack 測試標準以及長文本 Prompt 重排技術（如把關鍵證據置於開頭或結尾）。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
