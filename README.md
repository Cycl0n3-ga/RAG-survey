# RAG Survey

A structured literature survey and research map for Retrieval-Augmented Generation (RAG).

> **Want to read the survey, not browse the database? → [Start with the readable survey](./SURVEY.md).**

The repository now has two layers:

1. **Readable survey layer** — one continuous explanation of the field and the D01–D14 research map.
2. **Research database layer** — paper notes, domain pages, benchmarks, system maps, taxonomy audits, and project hypotheses.

> **Current taxonomy:** 14 Research Domains (D01–D14).  
> This is the only active top-level domain model in the repository.

## Read First

- **[RAG Survey — From Knowledge Construction to Evidence-Grounded Generation](./SURVEY.md)** ← main readable artifact (English)
- **[LLM 超長文件閱讀與撰寫技術全景 (深度調研報告)](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/LLM%20%E8%B6%85%E9%95%B7%E6%96%87%E4%BB%B6%E9%96%B1%E8%AE%80%E8%88%87%E6%92%B0%E5%AF%AB%E6%8A%80%E8%A1%93%E5%85%A8%E6%99%AF%20%28%E6%B7%B1%E5%BA%A6%E8%AA%BF%E7%A0%94%E5%A0%B1%E5%91%8A%29.md)** ← 繁體中文旗艦全景報告 (Traditional Chinese)
- [RAG Research Taxonomy & Domain Map](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20Research%20Taxonomy%20%26%20Domain%20Map.md)
- [RAG System Maps](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20System%20Maps.md)

## Research Database

- [Home / Knowledge Base Navigation](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/Home%20%28%E4%B8%BB%E7%9B%AE%E9%8C%84%E8%88%87%E7%9F%A5%E8%AD%98%E5%BA%AB%E5%B0%8E%E8%A6%BD%29.md)
- [Research Domains](./02%20-%20%E7%A0%94%E7%A9%B6%E9%A0%98%E5%9F%9F%E5%B0%88%E9%A1%8C%20%28Research%20Domains%29/README.md)
- [Literature Notes](./03%20-%20%E8%AB%96%E6%96%87%E5%BA%AB%20%28Literature%20Notes%29/README.md)
- [Benchmark Catalog](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20Benchmark%20Catalog.md)
- [Survey Papers Index](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/Survey%20Papers%20Index.md)
- [Pareto Trade-offs Analysis](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/%E6%8A%80%E8%A1%93%E5%85%A8%E6%99%AF%E8%88%87%20Pareto%20%E6%AC%8A%E8%A1%A1%E5%88%86%E6%9E%90%20%28Trade-offs%29.md)
- [Phase 1 Taxonomy Closure Audit](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/Phase%201%20Taxonomy%20Closure%20Audit%20-%202026-09-27.md)
- [Ideas & Hypotheses](./04%20-%20%E7%A0%94%E7%A9%B6%E6%83%B3%E6%B3%95%E8%88%87%E5%BE%85%E9%A9%97%E8%AD%89%E6%8F%90%E6%A1%88%20%28Ideas%20%26%20Hypotheses%29/README.md)

## Taxonomy at a Glance

For reading and presentation, use six survey-aligned macro groups. The **canonical internal taxonomy remains D01–D14**.

| Macro group | Internal Domains | Scope |
|---|---|---|
| Source & Knowledge Construction | D01–D04 | parsing/structure recovery, segmentation/granularity, extraction/consolidation, representation/indexing |
| Retrieval & Evidence Control | D05–D08 | query/retrieval, sufficiency & retrieval control, context construction/utilization, evidence reconciliation |
| Grounded Generation | D09 | grounded generation, attribution, long-form synthesis |
| Stateful & Agentic RAG | D10–D12 | knowledge/index maintenance, persistent memory, orchestration/action control |
| Evaluation | D13 | evaluation and failure attribution |
| Deployment & Trust | D14 | RAG systems/serving, security & integrity, privacy & access control |

## Core Classification Rules

- **Domain** = where the research problem occurs in the RAG lifecycle/system.
- **Topic** = a subproblem inside a Domain.
- **Paradigm Tag** = a cross-cutting method family, e.g. GraphRAG, Hierarchical RAG, Agentic RAG.
- **Adjacent Interface** = related but non-core RAG research, e.g. Long Context, KV Cache, General Agents.
- **Idea** = project-specific hypothesis; it is kept separate from published literature.

Key boundaries:

```text
Segmentation != Extraction != Representation
Relevance != Sufficiency != Utilization != Faithfulness
Source / Index Maintenance != Persistent Derived Memory
Domain != Paradigm Tag != Benchmark
```

## Current Corpus Snapshot

As of the metadata recount on **2026-10-02**:

- **205** literature notes with a `paper_id`
- **151** notes with D01–D14 primary domains
- **54** Adjacent/CROSS notes
- supplemental slide artifacts and abstract-only candidate lists are excluded

The D01–D06 topic maps now distinguish unit formation, semantic extraction, encoding/index organization, query-time retrieval, and evidence/control decisions. Huang and Huang's survey is included as a complementary process view, with its verified 2024 preprint content separated from 2026 publication metadata. The current domain counts and classification refresh are recorded in [Research Domains](./02%20-%20%E7%A0%94%E7%A9%B6%E9%A0%98%E5%9F%9F%E5%B0%88%E9%A1%8C%20%28Research%20Domains%29/README.md).

## Repository Layout

```text
SURVEY.md                     # readable end-to-end survey
00 - Navigation & MOC         # maps, indexes, taxonomy, audits
02 - Research Domains         # D01-D14 detailed domain pages
03 - Literature Notes         # paper-level research notes
04 - Ideas & Hypotheses       # project-specific proposals
Papers                        # local paper artifacts
```

The literature storage folders are organizational buckets only and are **not** a second taxonomy.
