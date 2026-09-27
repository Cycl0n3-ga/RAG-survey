---
title: "Domain 08 - Evidence Reconciliation"
domain_id: "D08"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Evidence Resolution"
last_updated: "2026-09-27"
---

# Domain 08 - Evidence Reconciliation

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

## Core Question
當候選 evidence 因內容、時間、版本、來源可靠度或適用條件而無法直接共同成立時，系統應如何偵測衝突並決定保留、降權、分流、合併或顯式揭露哪些 evidence？

## Includes
- temporal / version reconciliation
- knowledge conflict detection and resolution
- source reliability / credibility estimation
- provenance-aware resolution
- counter-evidence / contradiction handling
- applicability / scope-aware arbitration

## Excludes
- relevance ranking → D05
- evidence sufficiency / retrieve-more decision → D06
- context packing → D07
- source-of-truth version maintenance → D10
- malicious poisoning / prompt injection → D14

## Research Tracks
1. **Temporal & Version Reconciliation**
2. **Knowledge Conflict Resolution**
3. **Source Reliability & Provenance-Aware Resolution**

## Level-2 Topics
- Temporal Validity
- Version Reconciliation
- Knowledge Conflict Resolution
- Source Reliability / Credibility
- Provenance-Aware Resolution
- Counter-evidence Handling
- Applicability / Scope Arbitration

## Boundary
D08 only activates when evidence cannot simply coexist. `Relevance != Reliability`；`Sufficiency != Reconciliation`。D10 維護 versions，D08 在 query time 判斷哪一版本／哪一來源適用。

## Resolution Principle
- provenance：evidence 從哪裡來、經過哪些 derivation
- temporal validity：claim 在什麼時間成立
- applicability：在什麼產品／場域／條件下適用
- reliability：來源值得信任的程度

## Representative Notes

**Current primary-note coverage: 9**

- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2024-08) FreshLLMs - Refreshing Large Language Models with Search Engine Augmentation|FreshLLMs / FreshQA]] — temporal freshness.
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2026-08) Re3 - Relevance and Recency Retrieval for Mitigating Temporal Hallucination|Re³]] — relevance/recency arbitration.
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2026-07) When Facts Change - Temporal Knowledge Conflict Resolution in LLMs|When Facts Change]] — temporal/context-memory conflict benchmark.
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EMNLP 2024-11) Who's Who - Large Language Models Meet Knowledge Conflicts in Practice|Who's Who]] — practical knowledge conflicts.
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2025-07) FaithfulRAG - Fact-Level Conflict Modeling for Context-Faithful Retrieval-Augmented Generation|FaithfulRAG]] — fact-level context/parametric conflict.
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EMNLP 2025-11) MAGIC - A Multi-Hop and Graph-Based Benchmark for Inter-Context Conflicts in Retrieval-Augmented Generation|MAGIC]] — inter-context conflict benchmark.
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2026-07) KCR - Disentangling Reasoning Logic to Resolve Explicit Knowledge Conflicts|KCR]] — explicit conflict reasoning/resolution.
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2025-11) Retrieval-Augmented Generation with Estimation of Source Reliability|RA-RAG]] — source reliability.
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2025-10) VersionRAG - Version-Aware Retrieval-Augmented Generation for Evolving Documents|VersionRAG]] — emerging version-aware retrieval/reconciliation.

> [!NOTE]
> Temporal/version conflict, knowledge conflict and source reliability now have direct literature. Provenance lineage、approval-state、tenant/policy scope 與 applicability-aware arbitration 仍應標成 coverage gaps。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|D05 Query Understanding & Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06 Evidence Sufficiency & Adaptive Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation, Attribution & Long-form Synthesis]]
- [[02 - 研究領域專題 (Research Domains)/Domain 10 - Dynamic Knowledge & Index Maintenance|D10 Dynamic Knowledge & Index Maintenance]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D08 Evidence Reconciliation.**
> Earlier cleanup narrowed D08 too far to temporal/provenance only; general evidence conflict and source reliability are restored where literature supports them.

**Core question**：當候選 evidence 因內容、時間、版本、來源可靠度或適用條件而無法直接共同成立時，系統應如何偵測衝突並決定保留、降權、分流、合併或顯式揭露哪些 evidence？

**Activation rule**
> D08 only activates when evidence cannot simply coexist.

**Canonical Level-2**
- Temporal & Version Reconciliation
- Knowledge Conflict Resolution
- Source Reliability & Provenance-Aware Resolution
- Counter-evidence / contradiction handling

**Signal definitions**
- provenance = where evidence came from / derivation
- temporal validity = when a claim holds
- applicability = conditions/scope under which it applies
- reliability = how much a source should be trusted

**Hard boundary**
- D05 relevance ≠ reliability
- D06 sufficiency ≠ reconciliation
- D10 maintains versions; D08 reasons over versions at query time
- D14 handles malicious manipulation/security, not ordinary evidence disagreement

**Paper decisions**
- KEEP RA-RAG, When Facts Change, FreshLLMs, Re³.
- RA-RAG: D08 primary / D05 secondary; remove D14.
- ADD Who's Who (Findings EMNLP 2024), FaithfulRAG (ACL 2025), MAGIC (Findings EMNLP 2025), KCR (ACL 2026).
- provenance lineage / approval-state / applicability governance remain thin and should be marked gaps, not mature consensus.
