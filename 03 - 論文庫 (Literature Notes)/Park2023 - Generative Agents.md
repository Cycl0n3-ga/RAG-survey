---
title: "Generative Agents: Interactive Simulacra of Human Behavior"
authors: ["Joon Sung Park", "Joseph C. O'Brien", "Carrie J. Cai", "Meredith Ringel Morris", "Percy Liang", "Michael S. Bernstein"]
year: 2023
venue: "Stanford & Google / UIST 2023"
arxiv: "2304.03442"
url: "https://arxiv.org/abs/2304.03442"
pdf_file: "Papers/05 - Memory & Agents/(UIST 2023-10) Generative Agents - Interactive Simulacra of Human Behavior.pdf"
domains:
  - "[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]"
  - "[[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)]]"
tags:
  - paper
  - agent-memory-stream-&-reflection
---

# Generative Agents: Interactive Simulacra of Human Behavior

> [!INFO] 論文元數據 (Metadata)
> - **作者**：Joon Sung Park, Joseph C. O'Brien, Carrie J. Cai, Meredith Ringel Morris, Percy Liang, Michael S. Bernstein
> - **年份 / 會議**：2023 (Stanford & Google / UIST 2023)
> - **arXiv**：[2304.03442](https://arxiv.org/abs/2304.03442)
> - **論文分類**：`Agent Memory Stream & Reflection`
> - **本地 PDF 連結**：[[Papers/05 - Memory & Agents/(UIST 2023-10) Generative Agents - Interactive Simulacra of Human Behavior.pdf|開啟本地 PDF 檔案]]

---

## 一話摘要 (TL;DR)
**在虛擬小鎮中實現 25 個自主 Agent，提出包含記憶流（Memory Stream）、反思（Reflection）與規劃（Planning）的長期行為架構。**

---

## 核心痛點與研究背景 (Problem Statement)
LLM 缺乏長期的經驗累積與自我演化機制，在開放環境中無法維持長達數天的行事邏輯與性格一致性。

---

## 核心方法與技術架構 (Methodology & Architecture)
核心架構包含三要素：1. Memory Stream：按時間順序完整記錄感知到的所有事件；2. Retrieval：根據『時間新鮮度（Recency）』、『事件重要性（Importance）』與『語意相關度（Relevance）』加權提取記憶；3. Reflection：定期觸發高階抽象思考，將細碎記憶提煉為信念與世界觀；4. Planning：將信念轉化為行動大綱。

```mermaid
graph LR
    A["輸入文本 / Query"] --> B["Agent Memory Stream & Reflection 處理機制"]
    B --> C["優化後特徵 / 檢索結果 / 狀態"]
    C --> D["下游 LLM 解碼 / 最終輸出"]
```

---

## 關鍵優勢與權衡限制 (Strengths & Trade-offs)
優點：展現出驚人的長期湧現行為（自主傳播訊息、籌辦派對）；缺點：記憶流不斷線性增長，需要持續的反思摘要以防止檢索效率衰竭。

---

## 在長文件處理任務中的角色與啟發 (Implications for Long-Doc Processing)
現代 Agent 記憶架構（三維加權檢索與週期性反思）的靈魂先驅，廣泛啟發了長程任務自主智慧體的設計。

---

## 關聯領域與推薦閱讀 (Related Links)
- **所屬研究領域**：
  - [[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)]]
  - [[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)]]
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
