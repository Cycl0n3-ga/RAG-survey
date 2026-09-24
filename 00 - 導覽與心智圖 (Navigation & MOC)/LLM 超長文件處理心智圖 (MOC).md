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
graph TD
    DOC["超長文檔集 / 書籍 / 萬頁報告 (100k ~ 10M Tokens)"]

    subgraph Layer 1: 模型與序列計算層
        DOC --> LC["[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)\|Domain 01: Long Context]]<br>• FlashAttention-2/3<br>• Mamba / Selective SSM<br>• Ring Attention<br>• LongRoPE 2M"]
        DOC --> CP["[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)\|Domain 02: 多層次壓縮]]<br>• LLMLingua (Token Pruning)<br>• KIVI (2-bit KV Cache)<br>• SnapKV / PyramidKV<br>• RECOMP (Context Compressor)"]
    end

    subgraph Layer 2: 知識表示與檢索層
        DOC --> CK["[[02 - 研究領域專題 (Research Domains)/Domain 04 - Chunking 策略與知識擷取 (Proposition, Cross-chunk)\|Domain 04: 知識抽取與證據治理]]<br>• Dense X (Proposition)<br>• F/R/D/A/P/C/T 分類與操作語意<br>• 四層證據階梯 (Citation≠Entailment≠Authority≠Sufficiency)<br>• D-K-E-C-V-O 閉環與確定性修復迴圈"]
        CK --> RAG["[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)\|Domain 03: 先進 RAG]]<br>• ColBERT (Late Interaction)<br>• HyDE (Hypothetical Doc)<br>• Self-RAG (Reflection)<br>• Contextual Retrieval"]
        CK --> GRAG["[[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)\|Domain 05: Graph RAG]]<br>• Microsoft GraphRAG (Leiden)<br>• HippoRAG (PPR 聯想記憶)<br>• PropRAG / KG2RAG"]
    end

    subgraph Layer 3: 記憶與階層推理層
        RAG & GRAG --> MEM["[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)\|Domain 06: 外部記憶體]]<br>• MemGPT (LLM as OS)<br>• A-MEM (Cognitive Architecture)<br>• Working / Episodic / Semantic"]
        RAG & GRAG --> TREE["[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)\|Domain 07: 分層推理]]<br>• RAPTOR (Recursive Tree)<br>• Map-Reduce / Refine<br>• Tree-of-Thought"]
    end

    subgraph Layer 4: 長篇生成與智能體層
        MEM & TREE & LC --> GEN["[[02 - 研究領域專題 (Research Domains)/Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)\|Domain 08: 長篇生成撰寫]]<br>• STORM (Research-Outline-Write)<br>• Evidence Store<br>• Claim-Evidence Ledger"]
        GEN --> AGENT["[[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)\|Domain 09: Agentic 工作流]]<br>• Dynamic Planning<br>• Multi-Agent Debate<br>• Deep Research Protocol"]
    end

    subgraph Layer 5: 評估驗證與前沿藍圖
        AGENT --> EVAL["[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)\|Domain 10: 評估基準與安全]]<br>• RULER / InfiniteBench<br>• Lost in the Middle<br>• Pareto Frontier<br>• RAG Poisoning & Prompt Injection"]
        EVAL --> ROAD["[[02 - 研究領域專題 (Research Domains)/Domain 11 - 最具價值的研究方向與實驗設計 (Research Roadmap)\|Domain 11: 核心研究藍海與實驗]]<br>• Evidence Sufficiency<br>• Dynamic Routing<br>• Gold-Evidence Benchmark"]
    end
```

---

## 二、層級分類核心專題索引

### 1. 模型與運算層 (Model & Compute)
- **[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01: Long Context 與序列架構]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Vaswani2017 - Attention Is All You Need|Attention (Vaswani 2017)]]、[[03 - 論文庫 (Literature Notes)/Dao2022 - FlashAttention|FlashAttention (Dao 2022)]]、[[03 - 論文庫 (Literature Notes)/Gu2023 - Mamba Linear-Time Sequence Modeling|Mamba (Gu 2023)]]、[[03 - 論文庫 (Literature Notes)/Liu2023 - RingAttention|RingAttention (Liu 2023)]]、[[03 - 論文庫 (Literature Notes)/Ding2024 - LongRoPE 2M Context|LongRoPE (Ding 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 02 - 多層次壓縮技術 (Token, KV Cache, Context)|Domain 02: 多層次壓縮技術]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Jiang2023 - LLMLingua Prompt Compression|LLMLingua (Jiang 2023)]]、[[03 - 論文庫 (Literature Notes)/Jiang2023 - LongLLMLingua|LongLLMLingua (Jiang 2024)]]、[[03 - 論文庫 (Literature Notes)/Liu2024 - KIVI 2-bit KV Cache|KIVI 2-bit (Liu 2024)]]、[[03 - 論文庫 (Literature Notes)/Li2024 - SnapKV|SnapKV (Li 2024)]]、[[03 - 論文庫 (Literature Notes)/Cai2024 - PyramidKV|PyramidKV (Cai 2024)]]。

### 2. 資料與檢索層 (Data & Retrieval)
- **[[02 - 研究領域專題 (Research Domains)/Domain 03 - 先進 RAG 與檢索機制 (ColBERT, HyDE, Self-RAG)|Domain 03: 先進 RAG 與檢索機制]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Lewis2020 - Retrieval-Augmented Generation (RAG)|RAG (Lewis 2020)]]、[[03 - 論文庫 (Literature Notes)/Karpukhin2020 - Dense Passage Retrieval (DPR)|DPR (Karpukhin 2020)]]、[[03 - 論文庫 (Literature Notes)/Khattab2020 - ColBERT Late Interaction|ColBERT (Khattab 2020)]]、[[03 - 論文庫 (Literature Notes)/Gao2022 - HyDE Zero-Shot Dense Retrieval|HyDE (Gao 2022)]]、[[03 - 論文庫 (Literature Notes)/Asai2023 - Self-RAG|Self-RAG (Asai 2023)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 04 - Chunking 策略與知識擷取 (Proposition, Cross-chunk)|Domain 04: Chunking 策略、結構化知識擷取與證據治理]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Chen2023 - Dense X Proposition Retrieval|Dense X (Chen 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 05 - Graph RAG 與結構化知識 (Microsoft GraphRAG, HippoRAG)|Domain 05: Graph RAG 與結構化知識]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Edge2024 - Microsoft GraphRAG|Microsoft GraphRAG (Edge 2024)]]、[[03 - 論文庫 (Literature Notes)/Gutierrez2024 - HippoRAG|HippoRAG (Gutiérrez 2024)]]。

### 3. 記憶與推理層 (Memory & Reasoning)
- **[[02 - 研究領域專題 (Research Domains)/Domain 06 - 外部記憶體架構 (MemGPT, A-MEM, Working Memory)|Domain 06: 外部記憶體架構]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Packer2023 - MemGPT LLM as Operating System|MemGPT (Packer 2023)]]、[[03 - 論文庫 (Literature Notes)/Chik2025 - A-MEM Agentic Memory System|A-MEM (2025)]]、[[03 - 論文庫 (Literature Notes)/Park2023 - Generative Agents|Generative Agents (Park 2023)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 07 - 分層推理與樹狀檢索 (RAPTOR, Hierarchical QA)|Domain 07: 分層推理與樹狀檢索]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Sarthi2024 - RAPTOR Recursive Tree Retrieval|RAPTOR (Sarthi 2024)]]、[[03 - 論文庫 (Literature Notes)/Trivedi2022 - IRCoT Interleaving Retrieval and CoT|IRCoT (Trivedi 2022)]]。

### 4. 撰寫與智能體層 (Writing & Agents)
- **[[02 - 研究領域專題 (Research Domains)/Domain 08 - 長篇生成與報告撰寫 (STORM, Evidence Store, Ledger)|Domain 08: 長篇生成與報告撰寫]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Shao2024 - STORM Writing Wikipedia From Scratch|STORM (Shao 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 09 - Agentic 工作流與自主研究 (Planning, Multi-Agent)|Domain 09: Agentic 工作流與自主研究]]**

### 5. 評測、安全與前沿提案 (Evaluation, Safety & Roadmap)
- **[[02 - 研究領域專題 (Research Domains)/Domain 10 - 評估基準、系統工程與安全 (Benchmarks & Safety)|Domain 10: 評估基準、系統工程與安全]]**
  - 代表論文：[[03 - 論文庫 (Literature Notes)/Liu2023 - Lost in the Middle|Lost in the Middle (Liu 2023)]]、[[03 - 論文庫 (Literature Notes)/Bai2023 - LongBench Bilingual Multitask Benchmark|LongBench (Bai 2024)]]、[[03 - 論文庫 (Literature Notes)/An2023 - L-Eval Standardized Long Context Benchmark|L-Eval (An 2024)]]、[[03 - 論文庫 (Literature Notes)/Zhang2024 - InfiniteBench Beyond 100K|InfiniteBench (Zhang 2024)]]、[[03 - 論文庫 (Literature Notes)/Hsieh2024 - RULER What is the Real Context Size|RULER (Hsieh 2024)]]。
- **[[02 - 研究領域專題 (Research Domains)/Domain 11 - 最具價值的研究方向與實驗設計 (Research Roadmap)|Domain 11: 最具價值的研究方向與實驗設計]]**
