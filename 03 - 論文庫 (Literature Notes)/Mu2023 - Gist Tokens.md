---
title: "Learning to Compress Prompts with Gist Tokens"
authors: ["Jesse Mu", "Xiang Lisa Li", "Noah D. Goodman"]
year: 2023
venue: "NeurIPS 2023"
arxiv: "2304.08467"
url: "https://arxiv.org/abs/2304.08467"
pdf_file: "Papers/02 - Compression & KV Cache/(NeurIPS 2023-12) Learning to Compress Prompts with Gist Tokens.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]"
tags:
  - paper
  - learned-representation-compression
---

# Learning to Compress Prompts with Gist Tokens

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Jesse Mu, Xiang Lisa Li, Noah D. Goodman
> - **年份 / 會議**：2023 (NeurIPS 2023)
> - **arXiv**：[2304.08467](https://arxiv.org/abs/2304.08467)
> - **論文分類**：`Learned Representation Compression`
> - **本地 PDF 連結**：[[Papers/02 - Compression & KV Cache/(NeurIPS 2023-12) Learning to Compress Prompts with Gist Tokens.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**在 Prompt 末端插入可學習的 Gist Token，強制模型將整段長 Context 壓縮進少數隱向量中。**

---

## 核心痛點與研究背景 (Problem Statement)
現有壓縮依賴文字層面的刪除或重寫，而 Transformer 隱層維度本身具備更強大的資訊表徵潛力。

---

## 核心方法與技術架構 (Methodology & Architecture)
在預訓練模型中加入特定的 `<gist>` 標記，並修改 Attention Mask，強制後續的回答只能對 `<gist>` token 進行關注，而不能直接回溯原始 prompt 的前面 tokens。透過監督學習強迫 Gist token 吸收長 prompt 的全部語義。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Learned Representation Compression 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：極致壓縮比（數百 token 壓成 1~2 個向量）、加速顯著；缺點：需修改模型訓練注意力遮罩、缺乏可解釋性，且複雜邏輯的多跳線索難以全部無失真編碼進固定向量。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
為『隱空間 Token 壓縮（Soft Token / Memory Vector）』提供了標準範式，啟發了後續虛擬記憶體與持續狀態壓縮的研究。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
