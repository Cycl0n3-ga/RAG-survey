---
title: "A-MEM: Agentic Memory System with Hierarchical Structured Storage"
authors: ["Yung-Sung Chuang", "et al."]
year: 2025
venue: "arXiv 2025"
arxiv: "2502.05167"
url: "https://arxiv.org/abs/2502.05167"
pdf_file: "Papers/05 - Memory & Agents/(arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]"
tags:
  - paper
  - agentic-structured-memory
---

# A-MEM: Agentic Memory System with Hierarchical Structured Storage

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Yung-Sung Chuang, et al.
> - **年份 / 會議**：2025 (arXiv 2025)
> - **arXiv**：[2502.05167](https://arxiv.org/abs/2502.05167)
> - **論文分類**：`Agentic Structured Memory`
> - **本地 PDF 連結**：[[Papers/05 - Memory & Agents/(arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**針對超長任務 Agent 提出動態結構化階層記憶系統，結合情節記憶、語義記憶與程序記憶的自組織更新機制。**

---

## 核心痛點與研究背景 (Problem Statement)
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

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：記憶檢索極具結構性，能有效支援數週跨度的超長研究與撰寫任務；缺點：系統架構極其複雜，需要維護圖與向量的多重一致性。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
2025-2026 年長文處理從『單純檢索工具』邁向『具備認知自我狀態的自主實體』的代表性前沿工作。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
