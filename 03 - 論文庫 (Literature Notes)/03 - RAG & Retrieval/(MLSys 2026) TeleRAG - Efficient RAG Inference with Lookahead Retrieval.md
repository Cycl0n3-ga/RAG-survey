---
paper_id: "Lin2026_TeleRAG"
title: "TeleRAG: Efficient Retrieval-Augmented Generation Inference with Lookahead Retrieval"
authors:
  - "Chien-Yu Lin"
  - "Keisuke Kamahori"
  - "Yiyu Liu"
  - "Xiaoxiang Shi"
  - "Madhav Kashyap"
  - "Yile Gu"
  - "Rulin Shao"
  - "Zihao Ye"
  - "Kan Zhu"
  - "Rohan Kadekodi"
  - "Stephanie Wang"
  - "Arvind Krishnamurthy"
  - "Luis Ceze"
  - "Baris Kasikci"
year: 2026
publication_year: 2026
venue: "MLSys 2026"
doi: null
arxiv: null
url: "https://proceedings.mlsys.org/paper_files/paper/2026/hash/7fd522b89ac21009b7bbe7560a9a5add-Abstract-Conference.html"
pdf_file: null
tags:
  - paper
  - rag-systems
  - prefetching
  - scheduling
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
  - "lookahead_retrieval"
  - "prefetch_scheduling"
  - "rag_serving_latency"
---

# TeleRAG

Uses lookahead retrieval to prefetch required data from CPU to GPU in parallel with LLM generation, together with prefetch and cache-aware scheduling.

## Taxonomy decision
**Primary D14**: this is a serving/inference system contribution.
