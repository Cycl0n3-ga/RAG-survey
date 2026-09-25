---
title: "Canonical RAG Domain Migration Map"
tags: [migration, taxonomy, rag]
last_updated: "2026-09-25"
---

# Canonical RAG Domain Migration Map

本頁是遷移工作表。Legacy Domain 01–17 目前仍保留，避免破壞 Obsidian backlinks 與既有 paper metadata。

| Legacy Domain | Canonical destination | Action |
|---|---|---|
| 01 Long Context | Adjacent + D07 | 只保留 RAG interface；架構本身移出 core |
| 02 Compression | D07 + D14 + Adjacent | context / systems / KV 分流 |
| 03 Advanced RAG | D05 + D06 + D12 | retrieval / control / orchestration 分流 |
| 04 Chunking & KE | D02 + D03 | ✅ 第一階段內容拆分完成；legacy page 僅保留 backlinks |
| 05 GraphRAG | D03 + D04 + D05 + tag | 降為 paradigm |
| 06 Memory | D11 | persistent memory |
| 07 Hierarchical Reasoning | D04 + D05 + tag | representation / retrieval 分離 |
| 08 Long-form Generation | D09 | grounded synthesis |
| 09 Agentic Workflow | D12 | 收斂到 controller/orchestration |
| 10 Evaluation/System/Safety | D13 + D14 | evaluation 與 deployment/security 分離 |
| 11 Research Roadmap | Ideas & Hypotheses | 不再是 research domain |
| 12 Knowledge Extraction | D03 | merge |
| 13 Information Preservation | D03 + D13 | mechanism / evaluation 分流 |
| 14 Evidence Sufficiency | D06 | retain |
| 15 Temporal/Conflict/Provenance | D08 | retain |
| 16 Context Utilization/Faithfulness | D07 + D09 | utilization / output support 分離 |
| 17 Benchmarks/Evaluation | D13 | merge |

## Migration Status

- ✅ Canonical D01–D14 scaffold 已建立。
- ✅ 125 篇 Literature Notes 已寫入 Taxonomy v2 YAML metadata。
- ✅ Legacy Domain 04 已拆分至 D02 / D03。
- ⏳ 其餘 legacy domains 尚待逐一搬移與 backlinks 清理。

## Definition of Done
- Literature Notes 可解析到 canonical `primary_domain`。
- Home / MOC / Survey Index / Benchmark Catalog 不再把 legacy pages 當 canonical。
- GraphRAG / Hierarchical / Multimodal 等使用 paradigm tags。
- Long Context / KV / general model architecture 只保留 RAG interfaces。
- 最後才 archive/delete legacy pages。
