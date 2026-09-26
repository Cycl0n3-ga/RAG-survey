---
title: "RAG Paradigm Tags"
taxonomy_version: "v2"
tags: [taxonomy, rag, paradigm]
last_updated: "2026-09-25"
---

# RAG Paradigm Tags

Paradigm 是橫跨 lifecycle 的方法族，不是額外 Domain。

> [!IMPORTANT]
> 本表是 `paradigm_tags` 的**封閉字典（closed vocabulary）**。未列在表中的詞不要自行塞入 `paradigm_tags`：benchmark/survey 身分用 `artifact_type`，一般技術主題用 `tags` / `research_questions`，Long Context / KV / General Agents 等用 `adjacent_interfaces`。

| Tag | Definition | Typical Domains |
|---|---|---|
| graph_rag | graph/KG/community structure 支援 indexing、retrieval 或 synthesis | D03,D04,D05,D09,D10 |
| hierarchical_rag | tree / multi-resolution / parent-child structures | D02,D04,D05 |
| proposition_rag | proposition / atomic fact 作為 unit | D02,D03,D04,D05 |
| multi_hop_rag | evidence 需跨 documents / retrieval steps 組合 | D05,D06 |
| adaptive_rag | 依 query/state 動態決定 retrieval strategy | D06 |
| corrective_rag | retrieval/evidence quality 觸發修正 action | D06,D12 |
| reflective_rag | reflection/critique signals 控制 retrieval/generation | D06,D09,D12 |
| agentic_rag | controller 自主選 retrieval/tool/verify 等 action | D12 |
| memory_augmented_rag | persistent memory 與 retrieval/generation 共用 | D11,D12 |
| multimodal_rag | corpus/query/evidence/output 涉及多模態 | D01,D04,D05,D09 |
| temporal_rag | 顯式處理 time/version constraints | D08,D10 |
| citation_aware_rag | generation 綁定 citation/attribution | D09,D13 |
| long_form_rag | report-level evidence synthesis | D09,D13 |
| long_context_hybrid | long-context reading 與 RAG routing/packing | D05,D07,D14 |
| hybrid_rag | lexical/dense/graph/structured channels 融合 | D04,D05 |
| retrieval_augmented_training | retrieval 在 pretraining / instruction-tuning / joint retriever-reader training 中被納入學習流程 | D04,D05 |

## Metadata convention
```yaml
primary_domain: "D05"
secondary_domains:
  - "D04"
  - "D06"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
```

## Rule
新出現的 X-RAG 名稱，先判斷 Primary Domain，再加 tag；除非形成可區分、穩定且有文獻群支撐的新 lifecycle research problem，否則不新增 top-level Domain。
