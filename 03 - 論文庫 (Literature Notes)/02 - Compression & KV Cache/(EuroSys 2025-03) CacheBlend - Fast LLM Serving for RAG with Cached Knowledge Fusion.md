---
paper_id: "Yao2025_CacheBlend"
title: "CacheBlend: Fast Large Language Model Serving for RAG with Cached Knowledge Fusion"
authors:
  - "Jiayi Yao"
  - "Hanchen Li"
  - "Yuhan Liu"
  - "Siddhant Ray"
  - "Yihua Cheng"
  - "Qizheng Zhang"
  - "Kuntai Du"
  - "Shan Lu"
  - "Junchen Jiang"
year: 2024
publication_year: 2025
venue: "EuroSys 2025"
doi: "10.1145/3689031.3696098"
arxiv: "2405.16444"
url: "https://doi.org/10.1145/3689031.3696098"
pdf_file: null
tags:
  - paper
  - rag-systems
  - kv-cache
  - serving
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
  - "rag_kv_cache_reuse"
  - "ttft_reduction"
---

# CacheBlend

Reuses precomputed KV caches for multiple retrieved chunks while selectively recomputing a subset of tokens to recover cross-chunk dependencies.

## Taxonomy decision
**Primary D14 / A02 adjacent**: unlike generic KV compression, this is explicitly RAG multi-chunk serving.
