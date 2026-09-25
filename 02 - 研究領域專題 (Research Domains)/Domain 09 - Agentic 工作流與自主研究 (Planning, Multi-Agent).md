---
title: "Domain 09: Agentic 工作流與自主研究 (Autonomous Research, Planning, Multi-Agent Collaboration)"
tags:
  - "domain/agentic-workflows"
  - research-domain
---

# Domain 09: Agentic 工作流與自主研究 (Autonomous Research, Planning, Multi-Agent Collaboration)

> [!ABSTRACT] 核心問題意識 (Core Problem Statement)
> **面對開放性、未明確定義的高難度長文本任務，單一 Prompt 無法窮盡解法。如何設計具備規劃、工具呼叫、動態反思與多智能體協同的自主研究系統？**

---

### 一、核心問題意識：從單一模型到自主智能體系統
傳統 LLM 應用是單向管線（Pipeline）：輸入 Prompt $\rightarrow$ 模型輸出。
然而超長文件研究任務天生包含不確定性：
- 常常需要多輪查證：第一次檢索出的論文提到了一個未知術語，系統必須能自發暫停，啟動第二次專項檢索；
- 發現既定方案不可行時，必須具備動態重規劃（Re-planning）能力；
- 複雜長文任務涉及多元專業（文獻挖掘、代碼驗證、數據對比、寫作潤飾），單一 Agent 上下文容易混亂，需要**多智能體角色分工（Multi-Agent Specialization）**。

---

### 二、典型 Deep Research 智能體協同架構

```mermaid
graph TD
    User["使用者複雜研究指令"] --> Lead["Lead Research Agent (專案主控)"]
    
    Lead --> Plan["動態規劃模組 (Dynamic Planning)"]
    Plan --> Lead
    
    subgraph MultiAgentLayer["Multi-Agent Execution Layer"]
        Lead --> A1["Search & Crawler Agent<br/>(學術檢索與文獻下載)"]
        Lead --> A2["Fact-Check & Audit Agent<br/>(文獻真實性核查與年代比對)"]
        Lead --> A3["Synthesis & Analysis Agent<br/>(方法論提煉與矩陣對比)"]
        Lead --> A4["Report Writing Agent<br/>(大綱落實與章節撰寫)"]
    end
    
    A1 --> Env["外部工具環境<br/>(arXiv API / Web Search / Code Sandbox / Obsidian Vault)"]
    A2 --> Env
    A3 --> Env
    A4 --> Env
    Env --> A1
    Env --> A2
    Env --> A3
    Env --> A4
    
    A1 --> Critic["Critic & Verification Agent (獨立評審)"]
    A2 --> Critic
    A3 --> Critic
    A4 --> Critic
    Critic -->|通過| Lead
    Critic -->|未達標/存在證據缺口| Plan
```

---

### 三、關鍵核心機制

#### 1. 動態研究規劃 (Dynamic Research Planning)
- 進入研究前，先將宏觀主題解構為具備依賴關係的研究子任務（Task Dependency Graph）。
- 每一輪工具呼叫後，即時更新任務進度狀態（`pending`, `in_progress`, `completed`, `blocked`），並依據新發現動態調整或增刪後續任務。

#### 2. 工具調用與安全沙盒 (Tool Calling & Sandboxing)
- **學術接口調用**：arXiv API、Semantic Scholar、ACL Anthology。
- **程式碼沙盒執行**：即時撰寫 Python 腳本解析 PDF、提取統計數據、進行向量運算，確保研究數據的嚴謹與可重現。
- **檔案系統持久化**：將中間研究進展即時寫入 Markdown 筆記（如本 Obsidian Vault），防止長程任務因崩潰而丟失成果。

#### 3. 多角色協同 (Multi-Agent Debate & Reflection)
- 透過讓不同 Agent 分別扮演『贊成者』、『質疑審查者（Devil's Advocate）』與『仲裁者』，消除單一模型生成的認知偏誤與幻覺。

---

### 四、核心文獻與基準評測 (Key Literature & Benchmarks)
- **推理與行動交織 (Reasoning & Acting)**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(ICLR 2023-05) ReAct - Synergizing Reasoning and Acting in Language Models|ReAct (Yao et al., ICLR 2023)]] 將思維鏈（Thought）與行動（Action/Observation）動態交織，顯著降低獨立 CoT 的幻覺率。
- **語言強化學習反思 (Verbal Reinforcement Learning)**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NeurIPS 2023-12) Reflexion - Language Agents with Verbal Reinforcement Learning|Reflexion (Shinn et al., NeurIPS 2023)]] 無需微調權重，透過自然語言啟發式反思與情節記憶自我糾錯。
- **自主工具學習 (Self-supervised Tool Learning)**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NeurIPS 2023-12) Toolformer - Language Models Can Teach Themselves to Use Tools|Toolformer (Schick et al., NeurIPS 2023)]] 基於自監督損失差值自學何時呼叫計算機、搜尋引擎或維基百科 API。
- **多智能體長篇協同寫作**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models|STORM (Shao et al., NAACL 2024)]] 透過多角色視角探索與問答對話建構長篇結構化文章。
- **多輪環境智能體基準**：[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ICLR 2024-05) AgentBench - Evaluating LLMs as Agents|AgentBench (Liu et al., ICLR 2024)]] 首創涵蓋 OS、DB、KG、網頁等 8 大互動環境的客觀綜合評測體系。
- **多智能體對話與程式碼執行編排框架 (Multi-Agent Conversational Orchestration)**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2023-08) AutoGen - Enabling Next-Gen LLM Applications via Multi-Agent Conversation|AutoGen (Wu et al., 2023)]] 定義可對話智能體（ConversableAgent）與具備代碼沙盒執行能力的 UserProxyAgent，支援靜態與動態多智能體對話圖編排。
- **Agentic RAG 全景架構綜述 (Agentic RAG Survey)**：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2025-01) Agentic Retrieval-Augmented Generation - A Survey on Agentic RAG|Agentic RAG Survey (Singh et al., 2025)]] 系統性梳理從 Naive/Advanced/Modular RAG 向 Agentic RAG 演進之技術全景，定義動態規劃、工具調用、自我反思與多智能體協同架構。
- **真實高仿真網頁環境與功能性執行基準**：[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ICLR 2024-05) WebArena - A Realistic Web Environment for Building Autonomous Agents|WebArena (Zhou et al., ICLR 2024)]] 封裝 Magento、GitLab、Redmine 與 Postmill 等 4 大 Docker 網站，設計 812 個真實長視野任務與拒答校準驗證，以環境終態功能正確性為評測標準，展示出頂尖 LLM (GPT-4 14.41%) 與人類 (78.24%) 的顯著差距。

---

## 相關導覽與文獻快速跳轉
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
- **深度研究報告**：[[01 - 深度研究報告 (Deep Research Reports)/01 - LLM 超長文件閱讀與撰寫技術全景 (完整深度報告)|技術全景深度報告]]
- **權衡分析**：[[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術成熟度與 Pareto 權衡分析]]
