---
title: "HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models"
authors: ["Bernal Jiménez Gutiérrez", "Yiheng Shu", "Yu Gu", "Michihiro Yasunaga", "Yu Su"]
year: 2024
venue: "NeurIPS 2024"
arxiv: "2405.14831"
url: "https://arxiv.org/abs/2405.14831"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]"
tags:
  - paper
  - neurobiologically-inspired-graph-memory
---

# HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Bernal Jiménez Gutiérrez, Yiheng Shu, Yu Gu, Michihiro Yasunaga, Yu Su
> - **年份 / 會議**：2024 (NeurIPS 2024)
> - **arXiv**：[2405.14831](https://arxiv.org/abs/2405.14831)
> - **論文分類**：`Neurobiologically-Inspired Graph Memory`
> - **本地 PDF 連結**：[[Papers/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**模擬人類大腦海馬迴與新皮質聯想記憶機制，利用知識圖譜結合 Personalized PageRank 實現快速聯想多跳檢索。**

---

## 核心痛點與研究背景 (Problem Statement)
多跳複雜推理在傳統 RAG 中需要多次迭代呼叫 LLM，耗時且容易累積誤差；而全圖社群檢測成本又過於巨大。

---

## 核心方法與技術架構 (Methodology & Architecture)
仿生海馬迴索引（Hippocampal Indexing Theory）：新皮質保留原始文本，海馬迴充當聯想索引圖。利用 OpenIE 抽取知識圖譜，在檢索時將 Query 中的實體作為種子節點，在圖上執行個人化佩奇排名（Personalized PageRank, PPR）以極低成本模擬大腦突觸的聯想擴散，精準啟動多跳遠程關聯段落。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Neurobiologically-Inspired Graph Memory 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：單次檢索即可捕捉多跳關聯，在 MuSiQue 與 2Wiki 基準上超越 IRCoT 且速度快 10-30 倍；缺點：高度依賴實體抽取的精確度，面對抽象非實體問題效果有所下降。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
為神經生物學記憶機制在 LLM 長文本檢索架構中的實踐樹立了典範。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
