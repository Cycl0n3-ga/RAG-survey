---
paper_id: "Packer2023_MemGPT"
title: "MemGPT: Towards LLMs as Operating Systems"
authors:
  - "Charles Packer"
  - "Vivian Fang"
  - "Shishir G. Patil"
  - "Kevin Lin"
  - "Sarah Wooders"
  - "Joseph E. Gonzalez"
year: 2023
publication_year: 2024
venue: "ICML 2024 / arXiv"
doi: null
arxiv: "2310.08560"
url: "https://arxiv.org/abs/2310.08560"
pdf_file: "Papers/05 - Memory & Agents/(arXiv 2023-10) MemGPT - Towards LLMs as Operating Systems.pdf"
tags:
  - "paper"
  - "hierarchical-external-memory---llm-os"
verification_status: "verified"
last_verified: "2026-09-24"
taxonomy_version: "v2"
taxonomy_home: "D11"
primary_domain: "D11"
secondary_domains:
  - "D12"
paradigm_tags:
  - "memory_augmented_rag"
adjacent_interfaces: []

---

# MemGPT: Towards LLMs as Operating Systems

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Packer2023_MemGPT`
> - **作者**：Charles Packer, Vivian Fang, Shishir G. Patil, Kevin Lin, Sarah Wooders, Joseph E. Gonzalez
> - **預印本初次發布年份 (Preprint)**：2023
> - **正式發表年份 / 會議或期刊 (Venue)**：2024 (ICML 2024 / arXiv)
> - **DOI**：無
> - **arXiv**：[2310.08560](https://arxiv.org/abs/2310.08560)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/05 - Memory & Agents/(arXiv 2023-10) MemGPT - Towards LLMs as Operating Systems.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**借鑑傳統作業系統的階層式記憶體虛擬化技術，讓 LLM 自主管理主記憶體（Context）與外部磁碟存儲，實現無限上下文錯覺。**

---

## 研究背景與問題定義 (Problem Statement)
固定 Context Window 限制了長對話與長期文件的連續性，單純 RAG 缺乏自主狀態控制權與記憶主動寫入/更新機制。

---

## 核心方法與技術架構 (Methodology & Architecture)
將 LLM 視為 CPU，Context Window 視為 RAM，外部資料庫視為 Disk。定義三層記憶架構：1. Working Context（當前可見 prompt）；2. Recall Storage（對話歷史檢索庫）；3. Archival Storage（外部長期知識庫）。LLM 透過專用函數呼叫（Function Calling）自主執行 `memory_read`、`memory_write`、`memory_edit` 與分頁換入/換出（Paging）。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Hierarchical External Memory / LLM OS 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Figure 3 & Table 1 (Page 6-7): 於 Multi-session Chat 與長文文檔分析中，MemGPT 成功克服固定 context 限制，維持長達數萬輪的連續一致性，記憶體管理錯誤率低於 4%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：模型具備自我修正與長期狀態維護能力，理論上支援無限長壽命 Agent；缺點：LLM 需要耗費大量的思考步數管理自身記憶，在複雜任務中易發生記憶策略失調（Memory thrashing）。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
提出『LLM 即作業系統』的宏偉藍圖，是智慧體長期記憶體架構（Agentic Long-term Memory）的先驅代表作。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|D11 Memory-Augmented RAG]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
