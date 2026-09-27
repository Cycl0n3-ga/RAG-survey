---
title: "Phase 2 Legacy Forensic Audit - 2026-09-28"
taxonomy_version: "v2"
status: "phase2_closed"
date: "2026-09-28"
tags:
  - taxonomy
  - legacy
  - forensic-audit
  - rag
---

# Phase 2 Legacy Forensic Audit — 2026-09-28

> [!IMPORTANT]
> This audit compares the pre-cleanup **17-domain snapshot** against the closed D01–D14 Phase 1 taxonomy to determine whether legacy cleanup caused semantic loss.
>
> The goal is **not** to resurrect old domains. A legacy concept is restored only when it has independent value and is not already represented as a current Domain, Adjacent Interface, Paradigm Tag, Idea/Hypothesis, benchmark convention, or literature note.

## 1. Historical Baselines

Primary forensic baseline:

- **17-domain snapshot:** commit `48b5364a3151971b66e4f92bad930b983b4ee8f1`
  - commit message: `docs(navigation): update Home, MOC, Benchmark Catalog, Taxonomy Map, and AGENTS metadata for 17 domains`
  - date: 2026-09-24
- **Domain 12–17 introduction:** commit `3bd9d83d03e058a3f44a32f859a946a8b97775f2`
  - commit message: `feat(domains): add deep research domains 12-17 covering extraction, preservation, sufficiency, temporal conflict, utilization, and evaluation protocols`
- **Legacy-domain removal:** commit `006c9d1e9d77fd800e36c65fe0878301a14edc7b`
  - commit message: `refactor(taxonomy): remove legacy domains and keep only current taxonomy`
  - date: 2026-09-25

The current authoritative baseline is `master` after **Phase 1 closure**.

## 2. Verdict

**No old Domain needs to be restored.**

The 17-domain taxonomy mixed:
- core RAG lifecycle problems;
- generic long-context / inference topics;
- paradigms such as GraphRAG;
- project-specific governance hypotheses;
- evaluation conventions;
- research-roadmap material.

Phase 1 correctly separated those axes.

The forensic audit found **one genuinely useful legacy design pattern that had disappeared by name**:

> **Document State Store**

It has now been restored to
[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 05 - Evidence-Governed RAG 系統架構構想 (Delta Pipeline Design)|Idea 05]]
as a **project orchestration pattern**, not as literature-established D11 consensus.

All other high-value legacy concepts were found to be already preserved in current Domains, Adjacent Interfaces, Ideas, or benchmark/evaluation conventions.

## 3. Old D01–D17 Mapping

| Old domain | Legacy focus | Current disposition | Status |
|---|---|---|---|
| Old D01 | Long Context / Attention / SSM / Ring | A01 Long Context; A03 model architecture where applicable | **Intentionally adjacent** |
| Old D02 | Token / Context / KV compression | A02 generic compression/KV; RAG-specific context construction → D07 | **Absorbed / intentionally adjacent** |
| Old D03 | Advanced RAG / ColBERT / HyDE / Self-RAG | D04 representation, D05 retrieval/query, D06 retrieval control | **Absorbed** |
| Old D04 | Chunking + Knowledge Extraction | D02 segmentation, D03 extraction, D04 representation; project governance → Ideas 01/05 | **Absorbed / project hypotheses separated** |
| Old D05 | GraphRAG / structured knowledge | D03/D04/D05 + `graph_rag` paradigm tag | **Absorbed** |
| Old D06 | External Memory / MemGPT / A-MEM / Working Memory | D11 persistent memory; A01/A04 interfaces; Document State Store restored as project pattern | **Absorbed + one restore** |
| Old D07 | Hierarchical reasoning / RAPTOR / tree retrieval | D04 hierarchical representation, D05 retrieval; generic Map-Reduce/Refine/Tree-of-Thought patterns documented in D09/A04 interface | **Absorbed** |
| Old D08 | Long-form generation / Evidence Store / Ledger | D09 grounded long-form generation; Evidence Store optional; Claim-Evidence Ledger → Idea 04 | **Absorbed / project mechanism separated** |
| Old D09 | Agentic workflow / planning / multi-agent | D12 state→action orchestration; generic agent/tool work → A04 | **Absorbed** |
| Old D10 | Benchmarks + systems + safety | D13 evaluation; D14 systems/security/privacy; long-context eval → A01/D13 | **Correctly split** |
| Old D11 | Research roadmap / candidate gaps / experiment rules | Ideas 01–05 + Ideas README + Phase 1/2 audits | **Not a research Domain; preserved as research planning** |
| Old D12 | Knowledge Extraction & Typed Knowledge | D03; F/R/D/A/P/C/T explicitly kept as project hypothesis | **Absorbed** |
| Old D13 | Information Preservation & Cross-chunk Consolidation | D03 consolidation/fidelity + Idea 01 operational distortion taxonomy | **Absorbed** |
| Old D14 | Evidence Sufficiency & Adaptive Retrieval | D06; explicit five-state evidence-slot controller → Idea 02 | **Absorbed / project controller separated** |
| Old D15 | Temporal Conflict & Provenance-aware RAG | D08 Evidence Reconciliation; governance schema → Idea 03 | **Absorbed** |
| Old D16 | Context Utilization & Faithfulness | D07 utilization, D09 claim/citation boundary, D13 evaluation/oracles | **Correctly split** |
| Old D17 | RAG Benchmarks & Evaluation Protocols | D13 + Benchmark Catalog + evaluation conventions | **Absorbed** |

## 4. Detailed Semantic Preservation Checks

### 4.1 Old D12/D13 — extraction and information preservation

Legacy concepts verified as preserved:

- Retrieval Unit ≠ Semantic Unit
- Knowledge Type ≠ Authority / Usability
- entity / relation / event / proposition / claim extraction
- negation
- modality
- condition
- temporal scope
- numeric value/unit
- source/applicability scope
- coreference/entity drift
- unsupported cross-chunk edges
- cross-chunk consolidation and repair

The old eight-class distortion taxonomy is preserved in
[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 01 - Information-Preserving Knowledge Extraction|Idea 01]]
and is explicitly labeled a **project operational taxonomy**, rather than falsely presented as a field-wide standard.

### 4.2 Old D14 — evidence-slot sufficiency controller

The legacy five-state controller model:

```text
missing
retrieved-unverified
supported
conflicting
ineligible
```

is preserved in
[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 02 - Evidence Gap-Aware Adaptive Retrieval|Idea 02]].

The action semantics are also preserved:
- missing → targeted retrieval;
- retrieved-unverified → verify;
- conflicting → D08 reconciliation;
- ineligible → alternate source;
- all required slots supported → stop/generate;
- budget exhausted → abstain/escalate.

This was **not lost**; it was correctly demoted from alleged literature consensus to a falsifiable project-controller hypothesis.

### 4.3 Old D15 — temporal/provenance arbitration

The following are all preserved in current D08 and/or Idea 03:

- Valid Time vs Recorded/Record Time
- document version
- Draft / Under Review / Approved state
- applicable site / phase / environment / scope
- temporal supersedence
- scope divergence
- authority discrepancy
- genuine contradiction
- recency-only heuristic
- juxtaposition/disclosure
- provenance-aware arbitration
- counter-evidence stress testing

[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 03 - Provenance Temporal Conflict-Aware Evidence Resolution|Idea 03]]
correctly labels the unified evidence-object schema as **proposed**, not a standard RAG schema.

### 4.4 Old D16 — context utilization and faithfulness

Legacy concepts were redistributed by scientific intervention:

- Lost in the Middle / positional effects → D07/A01 interface
- distractor sensitivity → D07
- parametric-vs-retrieved factual conflict → D08
- citation / claim support generation → D09
- citation correctness / entailment evaluation → D13
- Gold Evidence / oracle isolation → D13

Current D09 explicitly retains:

```text
Citation present
    != citation relevant
    != citation entails claim
    != answer complete
```

Therefore the legacy citation-entailment distinction was **not lost**; it was moved out of the overly broad D16 into the appropriate generation/evaluation boundaries.

### 4.5 Old D17 — evaluation protocols

Current D13 retains all high-value protocol distinctions:

- Benchmark != Dataset != Metric != Evaluation Framework
- text-only evaluation boundary
- Gold Evidence / oracle intervention
- benchmark/pretraining contamination
- LLM-as-a-Judge bias
- dynamic API/version drift
- budget mismatch / cost-aware comparison
- nonlinear component interaction caveat
- meta-evaluation

[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 04 - End-to-End RAG Failure Attribution and Evidence Governance|Idea 04]]
also retains the layer-by-layer oracle localization design while warning that oracle gains are **not linearly additive responsibility percentages**.

## 5. Legacy Long-form / Hierarchical Patterns

The old taxonomy included generic long-document techniques that should not become standalone RAG Domains.

Current D09 explicitly preserves:

- Map-Reduce
- Refine
- tree-search / Tree-of-Thought-like orchestration
- outline-first / research-first writing
- evidence-first fixed-pool writing
- gap-aware iterative writing
- Evidence Store as an optional design
- Claim-Evidence Ledger as a project-specific mechanism
- revision / cross-section consistency

Thus the old long-form material was not deleted; it was normalized into D09 and its adjacent/general interfaces.

## 6. Restored Concept — Document State Store

Legacy old D06 described a persistent **Document State Store** for long-running deliverable generation:

- outline completion state;
- section progress;
- entities/terms already introduced;
- unresolved argument/evidence conflicts.

Unlike ordinary prompt context, this state survives across a long-running task. Unlike Evidence Store, it stores **workflow/deliverable state rather than evidence objects**.

This concept had no current exact equivalent by name and had independent practical value.

It has therefore been restored to Idea 05 with the following boundary:

```text
Document State Store
  = persistent workflow / deliverable progress state
  = D11 ↔ D12 ↔ D09 project interface

Evidence Store
  = candidate / verified evidence objects

Claim-Evidence Ledger
  = generated claims ↔ support / contradiction / verification

Canonical source/index state
  = D10

Current working prompt
  = D07 / A01
```

It remains a **project pattern requiring ablation**, not a literature-established architecture component.

## 7. Concepts Intentionally Not Restored as Core Domains

### Generic long-context/model architecture
Attention variants, SSMs, Ring Attention, positional extension and tokenizer-free architectures remain Adjacent Interfaces because they are model architecture, not RAG lifecycle problems.

### Generic KV/token compression
KIVI, SnapKV, PyramidKV and generic prompt compression remain A02 unless the intervention specifically constructs retrieved RAG context.

### Generic agent infrastructure
Tool calling, sandboxing, filesystem use and generic multi-agent frameworks remain A04 unless the research question concerns RAG evidence/action orchestration.

### Research roadmap
A roadmap is not a research Domain. Its hypotheses, baselines, oracles, ablations, budget parity and falsification criteria remain in Ideas/Hypotheses and project audit documents.

## 8. Over-pruning vs Correct Pruning

### Confirmed over-pruning already corrected in Phase 1
The main semantic over-pruning was **D08**: the cleanup had narrowed the domain too far toward temporal/provenance issues. Phase 1 restored broader evidence reconciliation:
- temporal/version conflict;
- general knowledge conflict;
- counter-evidence;
- source reliability.

### Correct pruning
The following removals were correct:
- long-context architecture from core RAG Domains;
- generic KV-cache compression from core RAG Domains;
- GraphRAG as a Domain rather than a paradigm;
- generic memory terminology without persistent-state lifecycle;
- “agentic” labeling based only on iteration/reflection/multiple agents;
- evaluation datasets being treated automatically as D13-primary;
- F/R/D/A/P/C/T, evidence-slot ledgers, governance schemas and deterministic invariants being presented as established literature consensus.

## 9. Phase 2 Closure Criteria

The 17 old Domains and the removed legacy MOC were inspected against current master.

For every substantive old research concept, one of the following destinations is now explicit:

1. current D01–D14;
2. Adjacent Interface;
3. Paradigm Tag;
4. Idea/Hypothesis;
5. evaluation/benchmark convention;
6. deliberately discarded duplicate/unsupported framing;
7. restored project pattern.

No old D15–D17 references are required on current master, and no legacy Domain file needs to be resurrected.

## 10. Closure

**Phase 2 status: CLOSED.**

The only unique legacy design pattern requiring restoration was **Document State Store**, now preserved in Idea 05.

The next planned step is:

> **Phase 3 — Literature Version & Duplicate Cleanup**

Phase 3 should systematically verify every literature note for:
- preprint → formal publication upgrades;
- duplicate paper versions;
- DOI/title/venue/author consistency;
- stale filenames that still encode arXiv/preprint status;
- duplicate notes whose semantic content should be merged before deletion.
