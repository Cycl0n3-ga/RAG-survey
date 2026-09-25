---
title: "Survey Papers Index"
tags:
  - survey
  - literature-map
  - rag
last_updated: "2026-09-26"
---

# Survey Papers Index

> [!IMPORTANT]
> **沒有主流 survey 使用與本 repo 完全相同的 D01–D14。**
> D01–D14 是本 repo 為了工程實驗、failure attribution 與文獻定位建立的 **operational taxonomy**，不是宣稱為社群標準。
> Survey 的用途是確認研究問題是否存在；方法細節、數字與 novelty 仍回到 primary paper。

## 1. Survey-aligned Macro Map

| Survey 常見研究軸 | 本 repo 對應 | 判定 |
|---|---|---|
| Corpus / parsing / indexing / retrieval-unit design | D01–D04 | 高度對齊；本 repo 拆得更細 |
| Query / retrieval / reranking / multi-hop / adaptive retrieval | D05–D06 | 高度對齊；D06 的「retrieval control」文獻較成熟 |
| Post-retrieval / context construction / evidence use | D07 | 高度對齊 |
| Temporal freshness / conflict / provenance | D08 | **部分對齊**；temporal/freshness 有文獻，authority arbitration 仍偏薄 |
| Grounded generation / attribution / long-form synthesis | D09 | 高度對齊 |
| Dynamic knowledge / index maintenance | D10 | **coverage gap**；目前缺真正 primary anchor |
| Memory / non-parametric knowledge | D11 | 對齊近年 memory / RAG 交界，但定義需涵蓋 interaction memory 與 derived persistent memory |
| Agentic / iterative orchestration | D12 | 高度對齊近年 Agentic RAG |
| Evaluation / benchmark / failure diagnosis | D13 | 高度對齊 |
| Systems / efficiency / robustness / security / trust | D14 | 有 survey 支撐 trustworthiness；systems/serving 仍需獨立補文獻 |

## 2. Core Survey Anchors — Keep This List Small

### General RAG
- **Gao et al. — Retrieval-Augmented Generation for Large Language Models: A Survey** (arXiv:2312.10997).  
  奠基性的 Naive / Advanced / Modular RAG 整理；保留作歷史 taxonomy anchor。  
  [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2023-12) Retrieval-Augmented Generation for Large Language Models - A Survey|Literature Note]]
- **Faridi et al. — Retrieval-Augmented Generation for Large Language Models: Evolution, Architectures, Applications, and Challenges (2020–2025)**, WIREs Data Mining and Knowledge Discovery, 2026, DOI: 10.1002/widm.70122.  
  作為目前較新的 broad survey anchor；涵蓋 retrieval granularity、indexing、reranking、context construction、retriever–generator integration、memory、agentic、GraphRAG、multimodal、evaluation 與 deployment risks。

### Retrieval / Reasoning / Agentic
- **Li et al. — A Survey of RAG-Reasoning Systems in Large Language Models**, Findings of EMNLP 2025, DOI: 10.18653/v1/2025.findings-emnlp.648.  
  支撐 D05/D06/D12 的 multi-step reasoning ↔ retrieval 交互。
- **Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG** (2025).  
  支撐 D12 的 planning、tool use、reflection 與 multi-agent orchestration。  
  [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2025-01) Agentic Retrieval-Augmented Generation - A Survey on Agentic RAG|Literature Note]]

### Structured Knowledge / GraphRAG
- **Peng et al. — Graph Retrieval-Augmented Generation: A Survey** (arXiv:2408.08921; later ACM TOIS).  
  以 Graph-Based Indexing → Graph-Guided Retrieval → Graph-Enhanced Generation 組織 GraphRAG；支撐 D03/D04/D05/D09 的 graph interface。  
  [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-08) Graph Retrieval-Augmented Generation - A Survey|Literature Note]]
- **Zhang et al. — A Survey of Generative Information Extraction**, COLING 2025.  
  支撐 D03 的 generative IE；**不**直接證明本 repo 的 information-preservation / F/R/D/A/P/C/T research proposal。

### Evaluation / Trustworthiness
- **Yu et al. — Evaluation of Retrieval-Augmented Generation: A Survey** (arXiv:2405.07437).  
  支撐 D13 的 retrieval / generation evaluation、faithfulness 與 benchmark design。  
  [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-05) Evaluation of Retrieval-Augmented Generation - A Survey|Literature Note]]
- **Ni et al. — Towards Trustworthy Retrieval Augmented Generation for Large Language Models: A Survey** (arXiv:2502.06872).  
  支撐 reliability、privacy、safety、fairness、explainability、accountability；主要對應 D14。

### Adjacent but Important
- **Abootorabi et al. — Ask in Any Modality: A Comprehensive Survey on Multimodal Retrieval-Augmented Generation**, Findings of ACL 2025.  
  Multimodal 是 cross-cutting paradigm，不需要另建 top-level Domain。
- Long-context surveys 屬 **A01 Adjacent Interface**；用來比較 Long Context vs RAG，不應重新變成 RAG core Domain。

## 3. What Is Not Yet Survey-Backed Enough

下列內容可以保留為研究問題，但不要寫成「survey 已形成共識」：

- **D03 information-preserving extraction / extraction-to-RAG error propagation**：保留為 Level-2 research lens + Idea 01。
- **D06 explicit evidence requirement → gap localization → targeted retrieval controller**：現有 adaptive-retrieval literature 主要解 retrieval control，不等同完整 evidence-set sufficiency。
- **D08 authority-weighted provenance arbitration**：temporal / freshness / version conflict 較有直接 literature；一般 authority resolver 仍薄。
- **D10 continual index maintenance**：目前 repo 尚缺 dedicated primary literature note。
- **D11 unified memory taxonomy**：interaction memory、model-side long-term memory、corpus/world memory 與 non-parametric continual knowledge 仍需用 memory survey / primary papers補齊。
- **D14 RAG serving systems**：trust/security 有 survey，但 serving / scheduling / caching / observability 應補 systems literature。

## 4. Version / Deduplication Rule

1. 同一論文的 arXiv → conference/journal：**只保留一份 note**，更新正式 venue / DOI，不另建新版 note。
2. v1 / v2 若只是同一工作的修訂：只保留最新正式版本。
3. 舊 paper 若有獨立歷史或方法貢獻（例如 DPR、ColBERT、RAG 2020、FlashAttention）：**不因年份舊而刪除**。
4. Survey 不追求數量；每條研究軸保留 **1 個最新 broad anchor + 必要的專項 survey** 即可。
5. Comparative study、benchmark、method paper 不因標題像 survey 就放進本頁。

## 5. Verified Source Entrypoints

- General RAG (Gao): https://arxiv.org/abs/2312.10997
- General RAG 2026 (Faridi et al.): https://doi.org/10.1002/widm.70122
- RAG-Reasoning Survey: https://aclanthology.org/2025.findings-emnlp.648/
- GraphRAG Survey: https://arxiv.org/abs/2408.08921
- Generative IE Survey: https://aclanthology.org/2025.coling-main.324/
- Multimodal RAG Survey: https://aclanthology.org/2025.findings-acl.861/
- RAG Evaluation Survey: https://arxiv.org/abs/2405.07437
- Trustworthy RAG Survey: https://arxiv.org/abs/2502.06872

> [!CAUTION]
> Survey 用來確認「研究線存在與如何被社群整理」；任何演算法流程、效果數字、速度、成本或 novelty claim 仍必須回 primary paper。
