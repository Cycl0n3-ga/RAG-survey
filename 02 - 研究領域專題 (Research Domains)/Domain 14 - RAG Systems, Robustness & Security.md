---
title: "Domain 14 - RAG Systems, Security & Privacy"
domain_id: "D14"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Deployment"
last_updated: "2026-09-27"
---

# Domain 14 - RAG Systems, Security & Privacy

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
當 RAG 引入外部資料庫、檢索階段、長 context、額外 state 與新的 attack surface 後，如何在真實部署條件下提供有效率、安全且具資料隔離能力的服務？

## Includes
- RAG serving latency / TTFT / throughput / scheduling
- RAG-specific caching and retrieval-generation overlap
- memory / resource allocation and cost/scalability
- corpus poisoning / retrieval manipulation
- retrieved-content indirect prompt injection
- adversarial retrieval / backdoor / integrity defenses
- membership inference / retrieval-data leakage
- access control / tenant isolation
- derived-data deletion / persistence governance
- observability / tracing

## Excludes
- ordinary relevance / ranking quality → D05
- distractor/context-utilization robustness → D07
- generator repair against misleading context → D09
- robustness/security benchmark measurement → D13
- generic KV/inference efficiency not RAG-specific → A02

## Research Tracks
1. **Systems & Serving**
2. **Security & Integrity**
3. **Privacy & Access Control**

## Level-2 Topics
- Serving Latency / Throughput / Cost
- Scheduling / Caching / Retrieval–Generation Overlap
- Observability / Tracing
- Corpus / Retrieval Integrity
- Retrieved-content Prompt Injection
- Corpus Poisoning / Adversarial Retrieval
- Retrieval-data Privacy
- Access Control / Tenant Isolation
- Derived-data Deletion / Persistence

## Boundary
Generic “robustness” is not a D14 catch-all. Only adversarial robustness / integrity under malicious manipulation belongs here by default. Evaluation-only security work → D13；generic serving/compression work → A02 unless it is RAG-specific systems research.

## Literature Coverage

**Current primary-note coverage: 8**

目前已有兩條直接 primary anchors：
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(SOSP 2025-10) METIS - Fast Quality-Aware RAG Systems with Configuration Adaptation|METIS]] — RAG-specific serving / scheduling / quality-latency configuration adaptation。
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(USENIX Security 2025-08) PoisonedRAG - Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models|PoisonedRAG]] — corpus / knowledge-base poisoning。

因此 D14 的 **systems** 與 **security** 已各有直接 anchor；仍缺的是 **observability/tracing 與 privacy/access-control/tenant isolation** 的 dedicated RAG primary literature。KIVI、CacheGen 等仍是 A02 inference/serving efficiency 與 D14 的交界。

Adjacent notes:
- [[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(ICML 2024-07) KIVI - A Tuning-Free Asymmetric 2-bit Quantization for KV Cache|KIVI]]
- [[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(SIGCOMM 2024-08) CacheGen - KV Cache Compression and Streaming for Fast Large Language Model Serving|CacheGen]]

## Systems and Threat Model

### End-to-end systems path

```text
T_total =
  T_parse/embed
+ T_search
+ T_rerank
+ T_prefill
+ T_decode
```

部署評估至少應同時報告 latency / TTFT、throughput、token / model-call budget、peak memory、indexing / serving cost；具體數值必須在同硬體、同模型、同 corpus 條件下比較。

### Threat classes

- **Retrieved-content / indirect prompt injection**：外部文件中的 instruction 被模型誤當成控制指令。
- **Corpus / retrieval poisoning**：攻擊者操控可被索引與召回的內容，使惡意或錯誤 evidence 被優先檢索。
- **Privacy / tenant leakage**：ACL、tenant isolation 或 retrieval filter 失敗，使不同 user / tenant 的資料交叉暴露。
- **Derived-data persistence**：原文刪除後，summary、embedding、knowledge graph edge 或 memory 仍殘留。
- **Noisy / adversarial evidence**：高度相關的 distractor、矛盾內容或偽來源導致 downstream generation 失真。

硬邊界：

```text
Retrieved Document ≠ Trusted Instruction
Retrieved Document ≠ Trusted Truth
```

目前 RAG-specific systems（METIS）與 security（PoisonedRAG）都已有 primary anchor；下一個真正缺口是 observability/tracing 與 privacy/access-control，而不是再堆一般 LLM serving papers。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy & Domain Map]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|RAG Adjacent Interfaces]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D14 RAG Systems, Security & Privacy.**
> Generic “robustness” is removed from the title to prevent D14 from becoming a catch-all. Only adversarial robustness / integrity under malicious manipulation belongs here by default.

**Core question**：當 RAG 引入外部資料庫、檢索階段、長 context、額外 state 與新的 attack surface 後，如何在真實部署條件下提供有效率、安全且具資料隔離能力的服務？

**Canonical tracks**
- Systems & Serving: latency/TTFT, throughput, scheduling, caching, retrieval–generation overlap, memory/resource allocation, cost/scalability
- Security & Integrity: corpus poisoning, retrieval manipulation, indirect prompt injection, backdoor/adversarial retrieval, defenses
- Privacy & Access Control: membership inference, retrieval-data leakage, access control, tenant isolation, deletion/persistence

**Robustness redistribution**
- irrelevant passage ranking/filtering → D05
- distractor handling/context utilization → D07
- generator revision against misleading context → D09
- robustness benchmark/measurement → D13
- malicious/adversarial integrity attacks/defenses → D14

**Paper decisions**
- METIS: KEEP D14; reduce secondaries substantially (D05/D06/D07 knobs are not independent contributions).
- PoisonedRAG: KEEP D14; remove D05/D13 secondary unless the note documents an independent contribution.
- ADD PipeRAG, CacheBlend, canonical 2026 RAGCache, TeleRAG as RAG-specific systems anchors.
- ADD direct RAG membership-inference/privacy and retrieved-content indirect-prompt-injection work.
- SafeRAG and “RAG LLMs are Not Safer” are evaluation-oriented → D13 primary / D14 secondary.
- Observability/tracing, tenant isolation and deletion governance remain comparatively thin.
