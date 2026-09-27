---
paper_id: "Jiang2025_PipeRAG"
title: "PipeRAG: Fast Retrieval-Augmented Generation via Algorithm-System Co-design"
authors:
  - "Wenqi Jiang"
  - "Shuai Zhang"
  - "Boran Han"
  - "Jie Wang"
  - "Bernie Wang"
  - "Tim Kraska"
year: 2024
publication_year: 2025
venue: "KDD 2025"
doi: "10.1145/3690624.3709194"
arxiv: "2403.05676"
url: "https://doi.org/10.1145/3690624.3709194"
pdf_file: null
tags:
  - paper
  - rag-systems
  - pipeline-parallelism
  - latency
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces:
  - "A02"
research_questions:
  - "retrieval_generation_pipelining"
  - "latency_quality_tradeoff"
---

# PipeRAG

Co-designs retrieval and generation using pipeline parallelism, flexible retrieval intervals and a performance model.

## Taxonomy decision
**Primary D14**: the central contribution is RAG system latency/quality co-design.
