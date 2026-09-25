---
title: "Domain 11 - Memory-Augmented RAG"
domain_id: "D11"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Cross-Lifecycle"
last_updated: "2026-09-26"
---

# Domain 11 - Memory-Augmented RAG

## Core Question
系統如何建立可跨 interaction / task 持續存在的 derived memory，並進行 write、link、retrieve、consolidate、evolve 與 forget，而不是每次只從原始 corpus 重新開始？

```mermaid
flowchart LR
    I["Interaction / Observation"] --> W["Memory Write"]
    W --> C["Consolidate"]
    C --> M["Persistent Memory"]
    M --> R["Memory Retrieval"]
    R --> CTX["Context / Action"]
    M -. "outdated / invalid" .-> F["Forget / Invalidate"]
    F -.-> M
```

## Includes
- episodic / semantic / task memory
- memory write / retrieval
- memory linking / consolidation / evolution
- forgetting / invalidation
- long-horizon interaction or task state
- derived corpus / world memory used as a persistent memory layer
- non-parametric continual knowledge integration
- memory provenance

## Excludes
- general corpus update → D10
- single-turn context packing → D07
- controller deciding when/how to use tools → D12

## Level-2 Topics
- Memory Write
- Memory Retrieval
- Episodic / Semantic Memory
- Consolidation
- Forgetting / Invalidation
- Long-horizon State
- Memory Provenance

## Boundary
```text
RAG corpus = canonical external source collection
Persistent memory = system-created state / derived representation that persists and evolves across interactions or tasks
Dynamic index = maintenance of the canonical external knowledge/index after source changes
```

## Representative Notes

**Current primary-note coverage: 6**

- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2023-10) MemGPT - Towards LLMs as Operating Systems|MemGPT]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NeurIPS 2023-12) LongMem - Augmenting Language Models with Long-Term Memory|LongMem]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(AAAI 2024-03) MemoryBank - Enhancing Large Language Models with Long-Term Memory|MemoryBank]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NeurIPS 2025-12) A-MEM - Agentic Memory for LLM Agents|A-MEM]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2024-09) MemoRAG - Moving towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery|MemoRAG]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models|From RAG to Memory]]

> [!NOTE]
> D11 不再只等同「個人對話記憶」。LongMem、MemoRAG、HippoRAG/From-RAG-to-Memory 類工作顯示，RAG literature 也會把 persistent non-parametric knowledge layer 視為 memory。D10 與 D11 的分界應看「是否在維護外部 canonical index」或「是否在形成系統自身持續演化的 memory state」。

## Memory Types and Governance Boundary
Memory 不應只用「向量庫」一詞概括。可用下列維度理解：

- **Working state**：本輪/短期 task state；若只存在 prompt/context，主要屬 D07/D12，而非 persistent memory。
- **Episodic memory**：過去 interaction / observation / trajectory。
- **Semantic memory**：從多次 interaction 整合出的穩定事實或概念。
- **Procedural / skill memory**：工具使用、policy、workflow 等「怎麼做」的知識；通常與 A04 General Agents / D12 相交。
- **Task / document state**：長時間任務的進度、已完成章節、未解決問題與一致性狀態。

### Memory governance

Persistent memory 還需要回答：
- 誰可以 write / read？
- 何時 consolidate / invalidate / forget？
- 原始 source 被刪除後，derived summary / fact / graph edge / memory 是否也要失效？
- 不同 user / tenant 的 memory 是否可能交叉檢索？
- memory update 是否保留 provenance 與 version？

這些治理問題與 D14 privacy/access control 交叉，但 memory lifecycle 本身仍屬 D11。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 10 - Dynamic Knowledge & Index Maintenance|D10 Dynamic Knowledge & Index Maintenance]]
- [[02 - 研究領域專題 (Research Domains)/Domain 12 - Agentic RAG & Orchestration|D12 Agentic RAG & Orchestration]]
