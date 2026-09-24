---
title: "LLM 超長文件處理心智圖 (MOC)"
tags:
  - moc
  - mindmap
---

# 🧠 LLM 超長文件處理全景心智圖 (Map of Content)

> [!TIP] 互動心智圖導覽
> 本心智圖完整覆蓋超長文本從『理解/閱讀』到『推理/撰寫』的五大垂直層次與 11 大研究主軸。
> 點擊心智圖下方的專題與論文連結，即可直接跳轉至各專題的深度技術剖析。

---

## 一、全景系統拓撲架構圖

```mermaid
flowchart TD
    subgraph layer_a["Layer A: 來源解析與結構化抽取 (Source Parsing & Extraction)"]
        DOC["原始長文件 / 企業文檔 (Corpus)"] --> PARSE["文件解析與閱讀順序 (DocLayNet)"]
        PARSE --> CHUNK["切塊與語意邊界 (LumberChunker / Late Chunking)"]
        CHUNK --> D12["Domain 12: 知識擷取與類型化知識<br/>(UIE / Proposition / F-R-D-A-P-C-T)"]
        D12 --> D13["Domain 13: 資訊保真與跨塊關聯整合<br/>(Dense X / PropRAG / CrossAug)"]
    end

    subgraph layer_b["Layer B: 知識表示與多解析度索引 (Representation & Indexing)"]
        D13 --> D04["Domain 04: 知識單元多元表示光譜"]
        D13 --> D05["Domain 05: Graph RAG (Microsoft GraphRAG / HippoRAG)"]
        D13 --> D02["Domain 02: 多層次壓縮技術 (Prompt / KV Cache)"]
        D13 --> D06["Domain 06: 外部記憶架構 (MemGPT / A-MEM)"]
        D13 --> D07["Domain 07: 分層推理與樹狀檢索 (RAPTOR)"]
    end

    subgraph layer_c["Layer C: 查詢理解與自適應檢索 (Query & Adaptive Retrieval)"]
        Q["使用者問題 / 報告義務 (User Query)"] --> D03["Domain 03: 先進 RAG 與檢索機制<br/>(DPR / ColBERT / HyDE)"]
        D03 --> D14["Domain 14: 證據充分性與自適應檢索<br/>(Slot Status / Gap Localization / Abstention)"]
    end

    subgraph layer_d["Layer D: 時序衝突與來源仲裁 (Conflict Resolution & Provenance)"]
        D14 --> D15["Domain 15: 時序衝突與來源仲裁 RAG<br/>(Valid Time / Version / Re3 / ConfRAG)"]
    end

    subgraph layer_e["Layer E: 上下文利用與長篇循證生成 (Utilization & Long-form Generation)"]
        D15 --> D16["Domain 16: 上下文利用率與生成忠實度<br/>(Lost in the Middle / Packing / Citation Entailment)"]
        D16 --> D08["Domain 08: 長篇生成與報告撰寫<br/>(STORM / Evidence Store / Ledger)"]
        D16 --> D01["Domain 01: Long Context 與序列架構 (Attention / Mamba)"]
        D08 --> D09["Domain 09: Agentic 工作流與自主研究"]
    end

    subgraph layer_f["Layer F: 評測基準與研究藍圖 (Evaluation & Roadmap)"]
        D08 --> D17["Domain 17: RAG 評測基準與評估協議<br/>(RAGChecker / RAGAS / Oracle Attribution)"]
        D17 --> D10["Domain 10: 評估基準、系統工程與安全"]
        D17 --> D11["Domain 11: 研究缺口與可反駁假設 (Roadmap)"]
        D11 -. 研究提案 .-> IDEA["04: 研究想法與待驗證提案 (Ideas & Hypotheses)"]
    end
```

**圖中節點對照**：全景涵蓋 17 大研究領域專題與 6 大垂直研究層次；未經文獻直接證實的組合機制集中收錄於 [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/README|Ideas & Hypotheses]]。

---

## 二、層級分類核心專題索引 (17 大研究領域)

### 1. 模型與運算層 (Model & Compute)
- **[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01: Long Context 與序列架構]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(NeurIPS 2017-12) Attention Is All You Need|Attention (Vaswani 2017)]]、[[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(NeurIPS 2022-12) FlashAttention - Fast and Memory-Efficient Exact Attention with IO-Awareness|FlashAttention (Dao 2022)]]、[[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(arXiv 2023-12) Mamba - Linear-Time Sequence Modeling with Selective State Spaces|Mamba (Gu 2023)]]、[[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICLR 2024-05) RingAttention with Blockwise Transformers for Near-Infinite Context|RingAttention (Liu 2023)]]、[[03 - 論文庫 (Literature Notes)/01 - Long Context & Sequence/(ICML 2024-07) LongRoPE - Extending LLM Context Window Beyond 2 Million Tokens|LongRoPE (Ding 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02: 多層次壓縮技術]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(EMNLP 2023-12) LLMLingua - Compressing Context for Accelerated Inference of Large Language Models|LLMLingua (Jiang 2023)]]、[[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(ACL 2024-08) LongLLMLingua - Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression|LongLLMLingua (Jiang 2024)]]、[[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(ICML 2024-07) KIVI - A Tuning-Free Asymmetric 2-bit Quantization for KV Cache|KIVI 2-bit (Liu 2024)]]、[[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(arXiv 2024-04) SnapKV - LLM Knows What You are Looking for Before Generation|SnapKV (Li 2024)]]、[[03 - 論文庫 (Literature Notes)/02 - Compression & KV Cache/(EMNLP 2024-11) PyramidKV - Dynamic KV Cache Compression based on Pyramidal Information Funneling|PyramidKV (Cai 2024)]]。

### 2. 來源解析、知識抽取與保真層 (Parsing, Extraction & Preservation)
- **[[02 - 研究領域專題 (Research Domains)/Domain 04 - Chunking 策略與知識擷取 (Proposition, Cross-chunk)|Domain 04: Chunking 策略與知識擷取]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA|Dense X (Chen 2024)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2024-11) LumberChunker - Long-Context LLMs as Modular Chunkers for Long-Document RAG|LumberChunker (Duarte 2024)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-09) Late Chunking - Contextual Chunk Embeddings for Retrieval|Late Chunking (Günther 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 12 - Knowledge Extraction & Typed Knowledge|Domain 12: 知識擷取與類型化知識表示]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2022-05) Unified Structure Generation for Universal Information Extraction|UIE (Lu 2022)]]、DocRED (2019)、MAVEN (2020)。
- **[[02 - 研究領域專題 (Research Domains)/Domain 13 - Information Preservation & Cross-chunk Consolidation|Domain 13: 資訊保真與跨塊關聯整合]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA|Dense X (Chen 2024)]]、PropRAG (EMNLP 2025)、CrossAug (2026)。

### 3. 檢索、圖結構與自適應控制層 (Retrieval, Graph & Adaptive Control)
- **[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03: 先進 RAG 與檢索機制]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(NeurIPS 2020-12) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks|RAG (Lewis 2020)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2020-11) Dense Passage Retrieval for Open-Domain Question Answering|DPR (Karpukhin 2020)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(SIGIR 2020-07) ColBERT - Efficient and Effective Passage Search via Contextualized Late Interaction over BERT|ColBERT (Khattab 2020)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2023-07) Precise Zero-Shot Dense Retrieval without Relevance Labels|HyDE (Gao 2022)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05: Graph RAG 與結構化知識]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-04) From Local to Global - A Graph RAG Approach to Query-Focused Summarization|Microsoft GraphRAG (Edge 2024)]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) HippoRAG - Neurobiologically Inspired Long-Term Memory for Large Language Models|HippoRAG (Gutiérrez 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 14 - Evidence Sufficiency & Adaptive Retrieval|Domain 14: 證據充分性與自適應檢索]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ICLR 2024-05) Self-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection|Self-RAG (Asai 2023)]]、[[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACL 2023-07) Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions|IRCoT (Trivedi 2022)]]、Adaptive-RAG (2024)、Evidence Sufficiency Benchmark (2026)。
- **[[02 - 研究領域專題 (Research Domains)/Domain 15 - Temporal Conflict & Provenance-aware RAG|Domain 15: 時序衝突與來源仲裁 RAG]]**
  - 代表論文：Re³ (ACL 2026)、ConfRAG (2024)。

### 4. 記憶與階層推理層 (Memory & Hierarchical Reasoning)
- **[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06: 外部記憶體架構]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2023-10) MemGPT - Towards LLMs as Operating Systems|MemGPT (Packer 2023)]]、[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2025-02) A-MEM - Agentic Memory System with Hierarchical Structured Storage|A-MEM (2025)]]、[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(UIST 2023-10) Generative Agents - Interactive Simulacra of Human Behavior|Generative Agents (Park 2023)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07: 分層推理與樹狀檢索]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) RAPTOR - Recursive Abstractive Processing for Tree-Organized Retrieval|RAPTOR (Sarthi 2024)]]。

### 5. 上下文利用、長篇撰寫與智能體層 (Utilization, Writing & Agents)
- **[[02 - 研究領域專題 (Research Domains)/Domain 16 - Context Utilization & Faithfulness|Domain 16: 上下文利用率與生成忠實度]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(TACL 2024-01) Lost in the Middle - How Language Models Use Long Contexts|Lost in the Middle (Liu 2023)]]、[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(arXiv 2024-08) RAGChecker - A Fine-grained Framework for Diagnosing Retrieval-Augmented Generation|RAGChecker (Ru 2024)]]、[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EACL 2024-03) RAGAS - Automated Evaluation of Retrieval Augmented Generation|RAGAS (Es 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)|Domain 08: 長篇生成與報告撰寫]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models|STORM (Shao 2024)]]、EviReport (ACL Findings 2026)、RAG4Reports (2026)、ReportLogic (ACL 2026)。
- **[[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09: Agentic 工作流與自主研究]]**

### 6. 評測基準、系統安全與研究藍圖 (Evaluation, Safety & Roadmap)
- **[[02 - 研究領域專題 (Research Domains)/Domain 17 - RAG Benchmarks & Evaluation Protocols|Domain 17: RAG 評測基準與評估協議]]**
  - 核心索引：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|RAG Benchmark Catalog (基準總索引)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10: 評估基準、系統工程與安全]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models|RULER (Hsieh 2024)]]、[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2024-08) LongBench - A Bilingual, Multitask Benchmark for Long Context Understanding|LongBench (Bai 2024)]]、[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2024-08) L-Eval - Instituting Standardized Evaluation for Long Context Language Models|L-Eval (An 2024)]]、[[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2024-08) InfiniteBench - Extending Long Context Evaluation Beyond 100K Tokens|InfiniteBench (Zhang 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 11 - 最具價值的研究方向與實驗設計 (Research Roadmap)|Domain 11: 最具價值的研究方向與實驗設計]]**
  - 專題提案：[[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/README|Ideas & Hypotheses (研究想法與提案庫)]]。
