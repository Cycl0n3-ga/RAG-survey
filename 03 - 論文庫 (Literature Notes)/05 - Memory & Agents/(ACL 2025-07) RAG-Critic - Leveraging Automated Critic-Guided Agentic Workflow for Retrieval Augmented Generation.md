---
paper_id: "Dong2025_RAGCritic"
title: "RAG-Critic: Leveraging Automated Critic-Guided Agentic Workflow for Retrieval Augmented Generation"
authors:
  - "Guanting Dong"
  - "Jiajie Jin"
  - "Xiaoxi Li"
  - "Yutao Zhu"
  - "Zhicheng Dou"
  - "Ji-Rong Wen"
year: 2025
publication_year: 2025
venue: "ACL 2025"
doi: "10.18653/v1/2025.acl-long.179"
arxiv: null
url: "https://aclanthology.org/2025.acl-long.179/"
pdf_file: null
tags:
  - paper
  - agentic-rag
  - critic
  - self-correction
  - failure-repair
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "method_paper"
research_questions:
  - "rag_error_critique"
  - "critic_guided_planning"
  - "error_driven_self_correction"
  - "agentic_rag_orchestration"
benchmark_ids:
  - "Natural Questions"
  - "TriviaQA"
  - "HotpotQA"
  - "2WikiMultiHopQA"
  - "ASQA"
  - "ELI5"
  - "Wizard of Wikipedia"
  - "FEVER"
  - "WikiASP"
metrics:
  - "task-specific QA / generation metrics"
taxonomy_version: "v2"
taxonomy_home: "D12"
primary_domain: "D12"
secondary_domains:
  - "D13"
  - "D06"
paradigm_tags:
  - "agentic_rag"
  - "reflective_rag"
adjacent_interfaces: []
---

# RAG-Critic: Leveraging Automated Critic-Guided Agentic Workflow for Retrieval Augmented Generation

## 一話摘要 (TL;DR)
RAG-Critic 將 **error diagnosis → critic feedback → planning → executable repair actions → re-evaluation** 串成 RAG-specific agentic self-correction loop；它的主要貢獻不是新的 retriever，而是讓 controller 根據細粒度 failure state 自動選擇修復流程。

## 核心架構
論文先從 9 個 RAG-related datasets、15 個 LLMs 蒐集錯誤案例，建立三層 error system；接著以 coarse-to-fine objective 對齊 error-critic model。最後由 planning model 根據 critic feedback 選擇與排列 action functions，產生可由 Python executor 執行的 repair program。

RAG Output
→ Error Critic
→ fine-grained feedback
→ Planning Agent
→ Action Program
→ Executor
→ Corrected RAG Output

作者定義超過 15 類可組合功能，包含 retrieval、query rewrite 等修復 action，因此系統的關鍵是 **state/error → action policy**，符合 D12 的 control-plane 定義。

## 主要實驗證據
- **Page 2**：error mining 涵蓋 9 datasets 與 15 LLMs；hierarchical error system 有 3 tiers、超過 4,000 個 fine-grained error labels。
- **Page 7, Table 4**：消融顯示移除 auto-planning 或 critic model 會在 NQ / TriviaQA / HotpotQA 上降低 F1；例如 HotpotQA 從完整系統的 51.2 降為 45.5（w/o Auto-Planning）與 47.0（w/o Critic Model）。
- 論文在 7 個 RAG-related datasets 做 end-to-end evaluation；結果支持 critic-guided repair 在其設定下有效，但不能推成所有 agentic workflow 都優於 fixed pipeline。

## Boundary
- **D12 primary**：planning/execution/self-correction 是最終方法 contribution。
- **D13 secondary**：hierarchical error mining 與 critic 是重要 diagnostic component。
- **D06 secondary**：部分 repair action 涉及 retrieve/rewrite，但不是單純 sufficiency/stopping 方法。
- 這篇不是 generic agent benchmark，也不是純 evaluation paper；它直接控制 RAG evidence/generation repair loop。

## Limitations / Trade-offs
- critic 錯判會把 planner 導向錯誤 repair path；
- 多輪 critique/planning/execution 增加 model calls 與 latency；
- error taxonomy 由資料驅動抽取再人工統整，coverage 仍受原始 datasets / LLM pool 分布限制；
- 不能用最終 task score 單獨判定 critic、planner、executor 各自貢獻，仍需 ablation / oracle diagnostics。

## Sources
- ACL Anthology: https://aclanthology.org/2025.acl-long.179/
- DOI: https://doi.org/10.18653/v1/2025.acl-long.179
- 本地 PDF：目前未存，使用 ACL Anthology 官方全文。
- [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|D12 Agentic RAG & Orchestration]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
