---
title: "L-Eval: Instituting Standardized Evaluation for Long Context Language Models"
authors: ["Chenxin An", "Shansan Gong", "Ming Zhong", "Xingjian Zhao", "Mukai Li", "Jun Zhang", "Lingpeng Kong", "Xipeng Qiu"]
year: 2023
venue: "Fudan University / ACL 2024"
arxiv: "2307.11088"
url: "https://arxiv.org/abs/2307.11088"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]"
tags:
  - paper
  - long-context-evaluation-standard
---

# L-Eval: Instituting Standardized Evaluation for Long Context Language Models

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Chenxin An, Shansan Gong, Ming Zhong, Xingjian Zhao, Mukai Li, Jun Zhang, Lingpeng Kong, Xipeng Qiu
> - **年份 / 會議**：2023 (Fudan University / ACL 2024)
> - **arXiv**：[2307.11088](https://arxiv.org/abs/2307.11088)
> - **論文分類**：`Long Context Evaluation Standard`
> - **本地 PDF 連結**：[[Papers/06 - Benchmarks & Evaluation/(ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**復旦大學提出包含封閉式問答與開放式問答的標準化長文本評測基準，解決長文本傳統 n-gram 指標失真的難題。**

---

## 核心痛點與研究背景 (Problem Statement)
長文本生成答案長度長、語義豐富，傳統 ROUGE/BLEU 無法準確判定模型是否真正推理出正確結論。

---

## 核心方法與技術架構 (Methodology & Architecture)
精選 18 個子任務，涵蓋 3k 到 200k tokens 的長度分佈。設計了雙重評估機制：1. 封閉式選擇題與提取題（可直接精確匹配驗證）；2. 經過人工細緻標註的長文本開放問答，結合基於規則的評分器與 LLM-as-a-Judge 混合評分方案。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Long Context Evaluation Standard 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：有效區分了『檢索能力』與『推理總結能力』，長度跨度大；缺點：LLM 裁判自身對超長 context 的偏誤仍需持續校準。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
促進了長文本評測從粗糙的詞頻比對走向語意等級標準化驗證的成熟階段。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
