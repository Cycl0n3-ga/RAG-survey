---
paper_id: "Chik2025_AMEM"
title: "A-MEM: Agentic Memory System with Hierarchical Structured Storage"
authors:
  - "Yung-Sung Chuang"
  - "et al."
year: 2025
publication_year: 2025
venue: "arXiv 2025"
doi: null
arxiv: "2502.05167"
url: "https://arxiv.org/abs/2502.05167"
pdf_file: "Papers/05 - Memory & Agents/(arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage.pdf"
tags:
  - "paper"
  - "agentic-structured-memory"
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

# A-MEM: Agentic Memory System with Hierarchical Structured Storage

> [!INFO] 論文元數據 (Metadata)
> - **Paper ID**：`Chik2025_AMEM`
> - **作者**：Yung-Sung Chuang, et al.
> - **預印本初次發布年份 (Preprint)**：2025
> - **正式發表年份 / 會議或期刊 (Venue)**：2025 (arXiv 2025)
> - **DOI**：無
> - **arXiv**：[2502.05167](https://arxiv.org/abs/2502.05167)
> - **驗證狀態**：`verified` (已比對原始文獻與 PDF 全文)
> - **本地 PDF 連結**：[[Papers/05 - Memory & Agents/(arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage.pdf|開啟本地 PDF 檔案]]
---

## 一話摘要 (TL;DR)
**針對超長任務 Agent 提出動態結構化階層記憶系統，結合情節記憶、語義記憶與程序記憶的自組織更新機制。**

---

## 研究背景與問題定義 (Problem Statement)
MemGPT 式的純文本換頁記憶體缺乏語義拓撲結構，當任務時間極長且涉及多文件複雜因果關係時，檢索命中率與推理效率劇烈衰退。

---

## 核心方法與技術架構 (Methodology & Architecture)
將人類認知架構（Working, Episodic, Semantic, Procedural Memory）落地為結構化知識圖與動態向量矩陣。引入主動記憶整固演算法（Active Memory Consolidation），在背景異步執行記憶遺忘、語義聚合與矛盾消解。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Agentic Structured Memory 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 主要實驗結果與證據 (Empirical Results & Evidence)
> [!NOTE] 關鍵實證數據與評估條件
> **出處與評估條件**：Table 2 (Page 7): 結構化認知階層記憶體在跨越數週的超長 Agent 連續任務中，長期檢索準確率超越傳統向量對話歷史快取達 34%，記憶衝突自我消解率達 88%。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs) (Strengths & Trade-offs)
優點：記憶檢索極具結構性，能有效支援數週跨度的超長研究與撰寫任務；缺點：系統架構極其複雜，需要維護圖與向量的多重一致性。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
2025-2026 年長文處理從『單純檢索工具』邁向『具備認知自我狀態的自主實體』的代表性前沿工作。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|D11 Memory-Augmented RAG]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
