---
title: "Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models"
authors: ["Yuhuai Shao", "Yucheng Jiang", "Theodore A. Kanell", "Peter Xu", "Omar Khattab", "Monica S. Lam"]
year: 2024
venue: "Stanford University / NAACL 2024"
arxiv: "2402.14207"
url: "https://arxiv.org/abs/2402.14207"
pdf_file: "Papers/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)|Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)]]"
tags:
  - paper
  - agentic-long-form-writing
---

# Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Yuhuai Shao, Yucheng Jiang, Theodore A. Kanell, Peter Xu, Omar Khattab, Monica S. Lam
> - **年份 / 會議**：2024 (Stanford University / NAACL 2024)
> - **arXiv**：[2402.14207](https://arxiv.org/abs/2402.14207)
> - **論文分類**：`Agentic Long-Form Writing`
> - **本地 PDF 連結**：[[Papers/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**史丹佛提出 STORM 系統，透過多視角訪談、大綱策劃與證據追溯，自動化撰寫萬字高結構維基百科全書級報告。**

---

## 核心痛點與研究背景 (Problem Statement)
直接要求 LLM 生成長篇文件會導致結構散亂、嚴重重複、內容空洞缺乏深度，且難以進行準確的引文來源歸屬。

---

## 核心方法與技術架構 (Methodology & Architecture)
將長文撰寫解構為三階段工程：1. Pre-writing（研究與訪談）：模擬各領域專家角色（Role-playing）向網路搜索引擎提問，進行多視角深度資訊蒐集；2. Outline Generation：彙整訪談所得證據，遞迴擬定結構嚴密的多級大綱；3. Article Generation & Polishing：依照大綱分段撰寫並自動嵌入引文連結，最後進行全篇語氣一致性潤飾。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Agentic Long-Form Writing 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：生成文章長度可達萬字以上，結構極其專業，資訊深度遠超單次 Prompt 生成；缺點：依賴大量外部檢索與多智慧體反覆呼叫，整體生成時間長（數分鐘至數十分鐘）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
超長篇報告生成的奠基石，確立了『先研究提問 $\rightarrow$ 次擬定大綱 $\rightarrow$ 再循證撰寫』的標準長文寫作流程。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)|Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
