---
title: "Domain 12 - Agentic RAG & Orchestration"
domain_id: "D12"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Cross-Lifecycle Control"
last_updated: "2026-09-25"
---

# Domain 12 - Agentic RAG & Orchestration

## Core Question
系統如何根據目前 state 自主選擇下一個 retrieval、tool、verification、memory 或 generation action？

```mermaid
flowchart LR
    S["Current State"] --> C["Controller / Policy"]
    C --> Q["Rewrite / Decompose"]
    C --> R["Retrieve / Route"]
    C --> V["Verify / Resolve"]
    C --> G["Generate / Abstain"]
    C --> M["Read / Write Memory"]
    Q -.-> S
    R -.-> S
    V -.-> S
    G -.-> S
    M -.-> S
```

## Includes
- controller / policy
- planning / routing
- tool selection
- iterative search-read-verify-generate loops
- multi-agent coordination
- workflow orchestration
- action selection from system state

## Excludes
- retrieval algorithm本身 → D05
- retrieve / retry / stop 的局部 sufficiency policy → D06
- persistent memory lifecycle本身 → D11
- generic agents without RAG-specific evidence control → A04

## Level-2 Topics
- Planning
- Controller / Policy
- Tool Use
- Routing
- Multi-Agent Coordination
- Research Workflow Orchestration
- Failure-aware Repair

## Boundary
**Agentic RAG 是 control plane，不是固定 pipeline stage。**  
若 paper 只改 retrieval method，不因為使用 agent loop 就自動歸 D12。

## Representative Notes

**Current primary-note coverage: 2**

- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2025-01) Agentic Retrieval-Augmented Generation - A Survey on Agentic RAG|Agentic RAG Survey]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) GraphReader - Building Graph-based Agent to Enhance Long-Context Abilities of Large Language Models|GraphReader]]

> [!NOTE]
> ReAct、Toolformer、AutoGen、WebGPT 等目前放在 A04 General Agents & Tool Use；只有當 contribution 直接控制 RAG evidence lifecycle 時，才歸 D12。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Adaptive Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 11 - Memory-Augmented RAG|D11 Memory-Augmented RAG]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|RAG Adjacent Interfaces]]
