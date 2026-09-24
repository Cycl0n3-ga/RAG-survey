---
title: "$\infty$Bench: Extending Long Context Evaluation Beyond 100K Tokens"
authors: ["Xinrong Zhang", "Yingfa Chen", "Shengding Hu", "Zihang Xu", "Junhao Chen", "Mao Sheng", "et al."]
year: 2024
venue: "Tsinghua University / ACL 2024"
arxiv: "2402.13718"
url: "https://arxiv.org/abs/2402.13718"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) InfiniteBench - Extending Long Context Evaluation Beyond 100K Tokens.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - paper
  - extreme-long-context-benchmark-(>100k)
---

# $\infty$Bench: Extending Long Context Evaluation Beyond 100K Tokens

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Xinrong Zhang, Yingfa Chen, Shengding Hu, Zihang Xu, Junhao Chen, Mao Sheng, et al.
> - **年份 / 會議**：2024 (Tsinghua University / ACL 2024)
> - **arXiv**：[2402.13718](https://arxiv.org/abs/2402.13718)
> - **論文分類**：`Extreme Long-Context Benchmark (>100K)`
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) InfiniteBench - Extending Long Context Evaluation Beyond 100K Tokens.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**清華與智譜提出首個平均長度突破 100k tokens（最高可達 500k）的極限長上下文評測基準 $\infty$Bench。**

---

## 核心痛點與研究背景 (Problem Statement)
2024 年各家宣稱支援 128k、200k 甚至 1M 上下文，但現有評測基準（如 LongBench）長度普遍在 32k 以下，無法檢驗模型在極限超長輸入下的真實推理崩潰點。

---

## 核心方法與技術架構 (Methodology & Architecture)
涵蓋 12 個核心任務，包含長篇小說多選題、長代碼依賴除錯、合成檢索、數學計算與長文本對話。所有數據集平均長度均超過 100k tokens，任務設計強制要求模型具備跨數萬字的訊息串聯與邏輯推演能力，而非單純的關鍵字匹配。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Extreme Long-Context Benchmark (>100K) 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：無情戳穿了大量宣稱支援 128k 但實際在 30k 以上就迅速崩潰的模型；缺點：評測成本極為高昂（推論一次 100k 序列需要龐大 GPU 資源與推論時間）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
100k+ 超長上下文時代最嚴格的試金石，直接推動了業界對極限長度注意力機制與 RoPE 插值技術的再優化。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
