---
title: "Paper Domain Migration Manifest"
taxonomy_version: "v2"
status: "yaml-applied"
paper_count: 125
last_updated: "2026-09-25"
---

# Paper Domain Migration Manifest

> [!IMPORTANT]
> 本表是 **125 篇現有 paper notes 的遷移 mapping**。它把「RAG core Domain」與「Adjacent Interface」分開，避免把 Long Context、KV Cache、general agents 等硬塞入 D01–D14。
>
> ✅ 2026-09-25：此 mapping 已寫回全部 125 篇 Literature Notes YAML：`taxonomy_home`、`primary_domain`、`secondary_domains`、`paradigm_tags`、`adjacent_interfaces`。Broad survey 若真正橫跨多層，可使用 `taxonomy_home: CROSS` 並將 `primary_domain: null`。

## Metadata target schema

```yaml
taxonomy_version: "v2"
taxonomy_home: "D05"   # 或 A01 / A02 / ... / CROSS
primary_domain: "D05"  # Axx / CROSS 時為 null
secondary_domains:
  - "D04"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
```

## Mapping

| Paper | Taxonomy Home | Primary Domain | Secondary Domains | Paradigm / Topic Tags | Adjacent Interfaces | Classification rationale |
|---|---|---|---|---|---|---|
| (ACL 2019-07) Transformer-XL - Attentive Language Models Beyond a Fixed-Length Context | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ACL 2020-07) Longformer - The Long-Document Transformer | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2020-04) Reformer - The Efficient Transformer | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2021-05) Rethinking Attention with Performers | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2024-05) Efficient Streaming Language Models with Attention Sinks | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2024-05) FlashAttention-2 - Faster Attention with Better Parallelism and Work Partitioning | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2024-05) LongLoRA - Efficient Fine-tuning of Long-Context Large Language Models | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2024-05) RingAttention with Blockwise Transformers for Near-Infinite Context | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICLR 2024-05) YaRN - Efficient Context Window Extension of Large Language Models | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ICML 2024-07) LongRoPE - Extending LLM Context Window Beyond 2 Million Tokens | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (NeurIPS 2017-12) Attention Is All You Need | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (NeurIPS 2020-12) Big Bird - Transformers for Longer Sequences | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (arXiv 2023-07) LongNet - Scaling Transformers to 1,000,000,000 Tokens | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (arXiv 2023-11) Advancing Transformer Architecture in Long-Context Large Language Models - A Survey | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (arXiv 2023-12) Mamba - Linear-Time Sequence Modeling with Selective State Spaces | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (arXiv 2024-04) Leave No Context Behind - Efficient Infinite Context Transformers with Infini-attention | A01 | — | — | long_context | A01 | Long-context / sequence architecture is adjacent to RAG. |
| (ACL 2024-08) LongLLMLingua - Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression | A02 | — | D07 | context_compression | A02 | General prompt/context compression; RAG context construction is secondary. |
| (EMNLP 2023-12) Compressing Context to Enhance Inference Efficiency of Large Language Models | A02 | — | D07 | context_compression | A02 | General prompt/context compression; RAG context construction is secondary. |
| (EMNLP 2023-12) LLMLingua - Compressing Context for Accelerated Inference of Large Language Models | A02 | — | D07 | context_compression | A02 | General prompt/context compression; RAG context construction is secondary. |
| (EMNLP 2024-11) PyramidKV - Dynamic KV Cache Compression based on Pyramidal Information Funneling | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (ICLR 2024-05) RECOMP - Improving Retrieval-Augmented LMs with Compression and Selective Augmentation | D07 | D07 | — | context_compression | A02 | Compresses retrieved context for RAG. |
| (ICML 2024-07) KIVI - A Tuning-Free Asymmetric 2-bit Quantization for KV Cache | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (NeurIPS 2023-12) H2O - Heavy-Hitter Oracle for Efficient Generative Inference of Large Language Models | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (NeurIPS 2023-12) Learning to Compress Prompts with Gist Tokens | A02 | — | D07 | context_compression | A02 | General prompt/context compression; RAG context construction is secondary. |
| (NeurIPS 2023-12) Scissorhands - Exploiting the Persistence of Importance Hypothesis for LLM KV Cache Compression at Test Time | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (NeurIPS 2024-12) MiniCache - KV Cache Compression in Depth Dimension for Large Language Models | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (SIGCOMM 2024-08) CacheGen - KV Cache Compression and Streaming for Fast Large Language Model Serving | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation | A02 | — | D14 | kv_cache, inference_efficiency | A02 | KV/cache serving efficiency is adjacent infrastructure. |
| (arXiv 2024-12) Byte Latent Transformer - Patches Scale Better Than Tokens | A03 | — | — | tokenization, model_architecture | A03 | General model/tokenization architecture. |
| (ACL 2023-07) Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions | D05 | D05 | D06, D12 | multi_hop_rag | — | Interleaved multi-step retrieval. |
| (ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (EMNLP 2023-12) Active Retrieval Augmented Generation | D06 | D06 | D05 | adaptive_rag | — | Active retrieval control. |
| (EMNLP 2024-11) Chain-of-Note - Enhancing Robustness in Retrieval-Augmented Language Models | D07 | D07 | D09 | evidence_utilization | — | Reading notes organize retrieved evidence. |
| (EMNLP 2024-11) LumberChunker - Long-Context LLMs as Modular Chunkers for Long-Document RAG | D02 | D02 | D05 | semantic_chunking | — | Chunk boundary selection. |
| (ICLR 2024-05) RA-DIT - Retrieval-Augmented Dual Instruction Tuning | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection | D06 | D06 | D05, D09 | adaptive_rag, reflective_rag | — | Adaptive retrieval and reflection control. |
| (ICML 2020-07) REALM - Retrieval-Augmented Language Model Pre-Training | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (ICML 2022-07) Improving Language Models by Retrieving from Trillions of Tokens | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (JMLR 2023-01) Atlas - Few-shot Learning with Retrieval Augmented Language Models | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (NAACL 2022-07) ColBERTv2 - Effective and Efficient Retrieval via Lightweight Late Interaction | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (NAACL 2024-06) Adaptive-RAG - Learning to Adapt Retrieval-Augmented Large Language Models through Question Complexity | D06 | D06 | D05 | adaptive_rag | — | Routes among retrieval strategies. |
| (NAACL 2024-06) REPLUG - Retrieval-Augmented Black-Box Language Models | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (NeurIPS 2020-12) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks | D05 | D05 | D09 | rag | — | Foundational RAG retrieval-generation architecture. |
| (NeurIPS 2024-12) RankRAG - Unifying Context Ranking with Retrieval-Augmented Generation in LLMs | D05 | D05 | D07, D09 | reranking | — | Ranking/retrieval contribution. |
| (SIGIR 2020-07) ColBERT - Efficient and Effective Passage Search via Contextualized Late Interaction over BERT | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (SIGIR 2022-07) SPLADE v2 - Sparse Lexical and Expansion Model for Information Retrieval | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (TMLR 2022-08) Unsupervised Dense Information Retrieval with Contrastive Learning | D05 | D05 | D04 | retrieval | — | Retrieval representation/training/ranking. |
| (arXiv 2023-12) Retrieval-Augmented Generation for Large Language Models - A Survey | cross-domain survey | — | D05, D06, D07, D09, D13 | survey | — | Broad RAG survey spans multiple lifecycle stages. |
| (arXiv 2024-01) Corrective Retrieval Augmented Generation | D06 | D06 | D05, D12 | corrective_rag | — | Corrective action after retrieval-quality assessment. |
| (arXiv 2024-05) Evaluation of Retrieval-Augmented Generation - A Survey | D13 | D13 | — | rag_evaluation, survey | — | Evaluation survey. |
| (arXiv 2024-06) LongRAG - Enhancing Retrieval-Augmented Generation with Long-context LLMs | D05 | D05 | D02, D07 | long_context_hybrid | A01 | Long-unit retrieval with long-context generation. |
| (arXiv 2024-09) Late Chunking - Contextual Chunk Embeddings for Retrieval | D02 | D02 | D04, D05 | contextual_chunking | — | Contextualized retrieval units. |
| (ACL 2019-07) DocRED - A Large-Scale Document-Level Relation Extraction Dataset | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (ACL 2020-07) A Joint Neural Model for Information Extraction with Global Features | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (ACL 2020-07) SciREX - A Challenge Dataset for Document-Level Information Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (ACL 2022-05) Unified Structure Generation for Universal Information Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (EMNLP 2019-11) Entity, Relation, and Event Extraction with Contextualized Span Representations | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (EMNLP 2020-11) MAVEN - A Massive General Domain Event Detection Dataset | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (EMNLP 2020-11) OpenIE6 - Iterative Grid Labeling and Coordination Analysis for Open Information Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (EMNLP 2021-11) REBEL - Relation Extraction By End-to-end Language generation | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA | D02 | D02 | D03, D04, D05 | proposition_rag, retrieval_granularity | — | Proposition retrieval granularity. |
| (EMNLP 2024-11) GraphReader - Building Graph-based Agent to Enhance Long-Context Abilities of Large Language Models | D12 | D12 | D04, D05 | graph_rag, agentic_rag | A01 | Graph-based agentic traversal. |
| (EMNLP 2025-11) PropRAG - Guiding Retrieval with Beam Search over Proposition Paths | D05 | D05 | D03, D04 | proposition_rag, multi_hop_rag | — | Retrieval over proposition paths. |
| (ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval | D04 | D04 | D05 | hierarchical_rag, multi_resolution | — | Tree-organized index/representation. |
| (ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models | D11 | D11 | D10 | memory_augmented_rag | A05 | Non-parametric continual memory. |
| (NAACL 2021-06) A Frustratingly Easy Approach for Entity and Relation Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (NAACL 2022-07) GenIE - Generative Information Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (NAACL 2025-05) Knowledge Graph-Guided Retrieval Augmented Generation | D05 | D05 | D04 | graph_rag, knowledge_graph_rag | — | KG-guided retrieval. |
| (NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering | D05 | D05 | D04 | graph_rag | — | Graph retrieval. |
| (NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models | D04 | D04 | D05, D11 | graph_rag, memory_augmented_rag | — | Graph-based memory/index. |
| (arXiv 2023-04) InstructUIE - Multi-task Instruction Tuning for Unified Information Extraction | D03 | D03 | — | knowledge_extraction | — | Information extraction. |
| (arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization | D04 | D04 | D03, D05, D09 | graph_rag, global_sensemaking | — | Graph/community index for global synthesis. |
| (arXiv 2024-08) Graph Retrieval-Augmented Generation - A Survey | D04 | D04 | D03, D05, D09 | graph_rag, survey | — | GraphRAG survey. |
| (arXiv 2024-10) LightRAG - Simple and Fast Retrieval-Augmented Generation | D04 | D04 | D05 | graph_rag | — | Graph-based index/retrieval. |
| (arXiv 2026-05) Beyond Chunk-Local Extraction - Cross-Chunk Graph Augmentation for GraphRAG | D03 | D03 | D04, D05 | graph_rag, cross_chunk | — | Cross-chunk extraction/augmentation. |
| (AAAI 2024-03) MemoryBank - Enhancing Large Language Models with Long-Term Memory | D11 | D11 | D12 | memory_augmented_rag | — | Persistent memory. |
| (ACL 2026-08) EFSG - Evidence-First Structured Generation for Multilingual RAG Report Generation | D09 | D09 | D07, D13 | long_form_rag, citation_aware_rag | — | Evidence-first report generation. |
| (ACL 2026-08) EviReport - From Reasoned Outlines to Evidence Tracked Long-Form Reports | D09 | D09 | D04, D06, D12 | long_form_rag, graph_rag, citation_aware_rag | — | Evidence-tracked report synthesis. |
| (ICLR 2023-05) ReAct - Synergizing Reasoning and Acting in Language Models | A04 | — | D12 | general_agent, tool_use | A04 | General agent/tool-use work. |
| (NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models | D09 | D09 | D05, D12 | long_form_rag, agentic_rag | — | Grounded long-form synthesis. |
| (NeurIPS 2023-12) LongMem - Augmenting Language Models with Long-Term Memory | D11 | D11 | D12 | memory_augmented_rag | — | Persistent memory. |
| (NeurIPS 2023-12) Reflexion - Language Agents with Verbal Reinforcement Learning | A04 | — | D12 | general_agent, tool_use | A04 | General agent/tool-use work. |
| (NeurIPS 2023-12) Toolformer - Language Models Can Teach Themselves to Use Tools | A04 | — | D12 | general_agent, tool_use | A04 | General agent/tool-use work. |
| (UIST 2023-10) Generative Agents - Interactive Simulacra of Human Behavior | A04 | — | D11, D12 | general_agent, memory | A04 | General agent architecture with memory. |
| (arXiv 2021-12) WebGPT - Browser-assisted question-answering with human feedback | A04 | — | D12 | general_agent, tool_use | A04 | General agent/tool-use work. |
| (arXiv 2022-03) Teaching language models to support answers with verified quotes | D09 | D09 | D05 | citation_aware_rag | — | Generation with verifiable quotations. |
| (arXiv 2023-08) AutoGen - Enabling Next-Gen LLM Applications via Multi-Agent Conversation | A04 | — | D12 | general_agent, tool_use | A04 | General agent/tool-use work. |
| (arXiv 2023-10) MemGPT - Towards LLMs as Operating Systems | D11 | D11 | D12 | memory_augmented_rag | — | Persistent memory. |
| (arXiv 2024-09) MemoRAG - Moving towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery | D11 | D11 | D12 | memory_augmented_rag | — | Persistent memory. |
| (arXiv 2024-11) OpenScholar - Synthesizing Scientific Literature with Retrieval-Augmented Language Models | D09 | D09 | D05, D12 | long_form_rag, agentic_rag | — | Scientific literature synthesis. |
| (arXiv 2025-01) Agentic Retrieval-Augmented Generation - A Survey on Agentic RAG | D12 | D12 | D05, D06, D11 | agentic_rag, survey | — | Agentic RAG survey. |
| (arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage | D11 | D11 | D12 | memory_augmented_rag | — | Persistent memory. |
| (ACL 2024-08) FreshLLMs - Refreshing Large Language Models with Search Engine Augmentation | D10 | D10 | D05, D08 | dynamic_rag, freshness | — | Freshness / knowledge update. |
| (ACL 2024-08) InfiniteBench - Extending Long Context Evaluation Beyond 100K Tokens | A01 | — | D13 | long_context_evaluation | A01 | Long-context benchmark. |
| (ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models | A01 | — | D13 | long_context_evaluation | A01 | Long-context benchmark. |
| (ACL 2024-08) LongBench - A Bilingual, Multitask Benchmark for Long Context Understanding | A01 | — | D13 | long_context_evaluation | A01 | Long-context benchmark. |
| (ACL 2024-08) RAGTruth - A Hallucination Corpus for Developing Trustworthy Retrieval-Augmented Language Models | D13 | D13 | D09 | rag_evaluation, hallucination | — | RAG hallucination evaluation. |
| (ACL 2026-08) AnalystBench - Benchmarking Professional Long-Form Report Generation with Web-Mined Multimodal Tasks | D13 | D13 | D09 | long_form_rag, benchmark | — | Long-form report benchmark. |
| (ACL 2026-08) Re3 - Relevance and Recency Retrieval for Mitigating Temporal Hallucination | D08 | D08 | D05, D13 | temporal_rag, recency | — | Temporal relevance/recency retrieval. |
| (ACL 2026-08) ReportLogic - Evaluating Logical Quality in Deep Research Reports | D13 | D13 | D09 | long_form_rag, benchmark | — | Long-form report benchmark. |
| (CMC 2026-08) Do LLMs Know When Evidence is Insufficient - An Evidence Sufficiency Benchmark | D13 | D13 | D06 | evidence_sufficiency, benchmark | — | Evidence sufficiency benchmark. |
| (COLING 2020-12) 2WikiMultiHopQA - A Multi-hop QA Dataset with Explanation Paths | D13 | D13 | D05 | multi_hop_rag, benchmark | — | Multi-hop benchmark/dataset. |
| (COLM 2024-10) MultiHop-RAG - Benchmarking Retrieval-Augmented Generation for Multi-Hop Queries | D13 | D13 | D05 | multi_hop_rag, benchmark | — | Multi-hop benchmark/dataset. |
| (EACL 2024-03) RAGAS - Automated Evaluation of Retrieval Augmented Generation | D13 | D13 | — | rag_evaluation | — | RAG evaluation. |
| (EACL 2026-03) T2-RAGBench - Benchmarking Text-and-Table Retrieval Augmented Generation | D13 | D13 | — | rag_evaluation | — | RAG evaluation. |
| (EMNLP 2018-10) HotpotQA - A Dataset for Diverse, Explainable Multi-hop Question Answering | D13 | D13 | D05 | multi_hop_rag, benchmark | — | Multi-hop benchmark/dataset. |
| (EMNLP 2022-12) ASQA - Factoid Questions Meet Long-Form Answers | D13 | D13 | D09 | long_form_rag, benchmark | — | Long-form answer benchmark. |
| (EMNLP 2023-12) Enabling Large Language Models to Generate Text with Citations | D09 | D09 | D13 | citation_aware_rag | — | Citation-grounded generation. |
| (EMNLP 2023-12) FActScore - Fine-grained Atomic Evaluation of Factual Precision in Long Form Text Generation | D13 | D13 | D09 | factuality, evaluation | — | Atomic factual precision evaluation. |
| (ICLR 2024-05) AgentBench - Evaluating LLMs as Agents | A04 | — | D13, D12 | agent_evaluation | A04 | General agent benchmark. |
| (ICLR 2024-05) WebArena - A Realistic Web Environment for Building Autonomous Agents | A04 | — | D13, D12 | agent_evaluation | A04 | General agent benchmark. |
| (KDD 2022-08) DocLayNet - A Large Human-Annotated Dataset for Document-Layout Analysis | D01 | D01 | D13 | document_structure, benchmark, multimodal_rag | — | Document layout analysis. |
| (NAACL 2021-06) KILT - A Benchmark for Knowledge Intensive Language Tasks | D13 | D13 | D05 | benchmark | — | Benchmark/dataset for retrieval/RAG. |
| (NAACL 2021-06) QASPER - A Dataset of Information-Seeking Questions and Answers Anchored in Research Papers | D13 | D13 | D05 | benchmark | — | Benchmark/dataset for retrieval/RAG. |
| (NAACL 2024-06) ARES - An Automated Evaluation Framework for Retrieval-Augmented Generation Systems | D13 | D13 | — | rag_evaluation | — | RAG evaluation. |
| (NeurIPS 2021-12) BEIR - A Heterogeneous Benchmark for Zero-shot Evaluation of Information Retrieval Models | D13 | D13 | D05 | benchmark | — | Benchmark/dataset for retrieval/RAG. |
| (NeurIPS 2024-12) CRAG - Comprehensive RAG Benchmark | D13 | D13 | D05 | benchmark | — | Benchmark/dataset for retrieval/RAG. |
| (PR 2023-12) Hierarchical Multimodal Transformers for Multi-Page DocVQA | D01 | D01 | D13 | multimodal_rag, document_qa | — | Multi-page document understanding. |
| (TACL 2022-05) MuSiQue - Multihop Questions via Single-hop Question Composition | D13 | D13 | D05 | multi_hop_rag, benchmark | — | Multi-hop benchmark/dataset. |
| (TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts | D07 | D07 | D13 | context_utilization | A01 | Context utilization / position effects. |
| (arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models | A01 | — | D13 | long_context_evaluation | A01 | Long-context benchmark. |
| (arXiv 2024-06) RAGBench - Explainable Benchmark for Retrieval-Augmented Generation Systems | D13 | D13 | — | rag_evaluation | — | RAG evaluation. |
| (arXiv 2024-08) RAGChecker - A Fine-grained Framework for Diagnosing Retrieval-Augmented Generation | D13 | D13 | — | rag_evaluation | — | RAG evaluation. |

## Review rules

1. 分類以 **primary contribution** 為準，不以資料夾名稱或標題中的 RAG 字樣為準。
2. Segmentation ≠ Extraction ≠ Representation。
3. Relevance ≠ Sufficiency ≠ Utilization ≠ Faithfulness。
4. Dynamic Index ≠ Persistent Memory。
5. GraphRAG / Hierarchical RAG / Adaptive RAG / Multimodal RAG 等是 orthogonal paradigms；以 tag 表示。
6. A01–A05 是 adjacent interfaces，不是 D01–D14 的延伸編號。
