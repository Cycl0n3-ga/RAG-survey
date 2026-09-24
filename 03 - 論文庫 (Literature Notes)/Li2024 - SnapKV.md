---
title: "SnapKV: LLM Knows What You are Looking for Before Generation"
authors: ["Yuhong Li", "Yingbing Huang", "Bowen Yang", "Bolei Ma", "Chenghao Cui", "et al."]
year: 2024
venue: "arXiv 2024"
arxiv: "2404.14469"
url: "https://arxiv.org/abs/2404.14469"
pdf_file: "Papers/02 - Compression & KV Cache/(arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]"
tags:
  - paper
  - kv-cache-pruning
---

# SnapKV: LLM Knows What You are Looking for Before Generation

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Yuhong Li, Yingbing Huang, Bowen Yang, Bolei Ma, Chenghao Cui, et al.
> - **年份 / 會議**：2024 (arXiv 2024)
> - **arXiv**：[2404.14469](https://arxiv.org/abs/2404.14469)
> - **論文分類**：`KV Cache Pruning`
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**利用 Prompt 末端觀察窗口的注意力分佈，在 Prefill 階段精準挑選核心 KV 特徵，剪掉 80% 以上的歷史快取。**

---

## 核心痛點與研究背景 (Problem Statement)
長文本在 Prefill 之後，KV Cache 隨長度呈線性增長，然而大部分歷史 token 在生成過程中極少被再次關注（注意力稀疏性）。

---

## 核心方法與技術架構 (Methodology & Architecture)
發現 LLM 在 Prefill 階段的末尾幾個 token（Observation Window）會自發對全文進行全域檢索，其注意力特徵能高度預測後續生成所需的重要歷史區塊。SnapKV 藉此挑選出每一層、每個 Attention Head 最重要的局部特徵聚類並永久保留，其餘 KV 直接丟棄。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["KV Cache Pruning 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：生成階段顯存恆定、推論吞吐量提升 3-4x；缺點：如果後續多輪對話中提問轉移了主題，先前被丟棄的 KV Cache 無法找回，必須重新 Prefill。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
開啟了『動態注意力引導的 KV 快取剪枝』新方向，是現代長文邊緣推論與高併發伺服器的重要核心組件。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
