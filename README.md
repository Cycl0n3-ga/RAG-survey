# RAG Survey

A structured literature survey and research map for Retrieval-Augmented Generation (RAG).

> **Current taxonomy:** 14 Research Domains (D01–D14).  
> This is the only active top-level domain model in the repository.

## Start Here

- [Home](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/Home%20%28%E4%B8%BB%E7%9B%AE%E9%8C%84%E8%88%87%E7%9F%A5%E8%AD%98%E5%BA%AB%E5%B0%8E%E8%A6%BD%29.md)
- [RAG Research Taxonomy & Domain Map](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20Research%20Taxonomy%20%26%20Domain%20Map.md)
- [RAG System Maps](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20System%20Maps.md)
- [Research Domains](./02%20-%20%E7%A0%94%E7%A9%B6%E9%A0%98%E5%9F%9F%E5%B0%88%E9%A1%8C%20%28Research%20Domains%29/README.md)
- [Literature Notes](./03%20-%20%E8%AB%96%E6%96%87%E5%BA%AB%20%28Literature%20Notes%29/README.md)
- [Benchmark Catalog](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20Benchmark%20Catalog.md)
- [Survey Papers Index](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/Survey%20Papers%20Index.md)
- [Pareto Trade-offs Analysis](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/%E6%8A%80%E8%A1%93%E5%85%A8%E6%99%AF%E8%88%87%20Pareto%20%E6%AC%8A%E8%A1%A1%E5%88%86%E6%9E%90%20%28Trade-offs%29.md)
- [Ideas & Hypotheses](./04%20-%20%E7%A0%94%E7%A9%B6%E6%83%B3%E6%B3%95%E8%88%87%E5%BE%85%E9%A9%97%E8%AD%89%E6%8F%90%E6%A1%88%20%28Ideas%20%26%20Hypotheses%29/README.md)

## Taxonomy at a Glance

For reading and presentation, use six survey-aligned macro groups. The **canonical internal taxonomy remains D01–D14**.

| Macro group | Internal Domains | Scope |
|---|---|---|
| Source & Knowledge Construction | D01–D04 | ingestion, segmentation, extraction, representation, indexing |
| Retrieval & Evidence Control | D05–D08 | query, retrieval, adaptive retrieval, context/evidence validation |
| Grounded Generation | D09 | grounded generation, attribution, long-form synthesis |
| Stateful & Agentic RAG | D10–D12 | dynamic knowledge, memory, orchestration |
| Evaluation | D13 | evaluation and failure attribution |
| Deployment & Trust | D14 | systems, robustness, privacy, security |

Full definitions and boundaries: [RAG Research Taxonomy & Domain Map](./00%20-%20%E5%B0%8E%E8%A6%BD%E8%88%87%E5%BF%83%E6%99%BA%E5%9C%96%20%28Navigation%20%26%20MOC%29/RAG%20Research%20Taxonomy%20%26%20Domain%20Map.md) and [Research Domains](./02%20-%20%E7%A0%94%E7%A9%B6%E9%A0%98%E5%9F%9F%E5%B0%88%E9%A1%8C%20%28Research%20Domains%29/README.md).

## Classification Rules

- **Domain** = where the research problem occurs in the RAG lifecycle/system.
- **Topic** = a subproblem inside a Domain.
- **Paradigm Tag** = a cross-cutting method family, e.g. GraphRAG, Hierarchical RAG, Agentic RAG.
- **Adjacent Interface** = related but non-core RAG research, e.g. Long Context, KV Cache, General Agents.
- **Idea** = project-specific hypothesis; it is kept separate from published literature.

Key boundaries:

```text
Segmentation != Extraction != Representation
Relevance != Sufficiency != Utilization != Faithfulness
Dynamic Index != Persistent Memory
Domain != Paradigm Tag != Benchmark
```

## Repository Layout

```text
00 - Navigation & MOC
02 - Research Domains          # D01-D14
03 - Literature Notes         # paper notes; storage folders are not Domains
04 - Ideas & Hypotheses       # project proposals / research ideas
Papers                         # local paper artifacts
```

The literature storage folders (Long Context, Compression/KV, RAG/Retrieval, Knowledge/Graph, Memory/Agents, Benchmarks/Evaluation) are organizational buckets only and are **not** a second taxonomy.
