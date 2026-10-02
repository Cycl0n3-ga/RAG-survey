---
title: "Survey Papers Index"
tags:
  - survey
  - literature-map
  - rag
last_updated: "2026-10-02"
---

# Survey Papers Index

> [!IMPORTANT]
> **沒有主流 survey 使用與本 repo 完全相同的 D01–D14。**
> D01–D14 是本 repo 為了工程實驗、failure attribution 與文獻定位建立的 **operational taxonomy**，不是宣稱為社群標準。
> Survey 的用途是確認研究問題是否存在；方法細節、數字與 novelty 仍回到 primary paper。

## 1. Survey-aligned Macro Map

| Survey 常見研究軸 | 本 repo 對應 | 判定 |
|---|---|---|
| Corpus / parsing / indexing / retrieval-unit design | D01–D04 | indexing 與 retrieval-unit design 有 broad survey 關聯；D01 parsing、D03 extraction/consolidation 的專門 coverage 須另核，不能由 pre-retrieval 名稱一併證明 |
| Query / retrieval / reranking / multi-hop / adaptive retrieval | D05–D06 | 高度對齊；D06 的「retrieval control」文獻較成熟 |
| Post-retrieval / context construction / evidence use | D05–D07 | **依研究問題拆分**：relevance reranking / filtering 屬 D05；retrieval trigger / retry / stop 屬 D06；context packing / compression / utilization 屬 D07，不能把所有 post-retrieval 歸 D07 |
| Temporal freshness / conflict / provenance | D08 | **部分對齊**；temporal/freshness/conflict 與 source reliability 已有文獻，provenance lineage / approval / scope arbitration 仍偏薄 |
| Grounded generation / attribution / long-form synthesis | D09 | 高度對齊 |
| Dynamic knowledge / index maintenance | D10 | **部分對齊**；Wu et al. 2026 survey 有 knowledge-base update section，AURORA 提供 direct primary anchor |
| Memory / non-parametric knowledge | D11 | 對齊近年 memory / RAG 交界，但定義需涵蓋 interaction memory 與 derived persistent memory |
| Agentic / iterative orchestration | D12 | 高度對齊近年 Agentic RAG |
| Evaluation / benchmark / failure diagnosis | D13 | 高度對齊 |
| Systems / efficiency / robustness / security / trust | D14 | trust/security 有 survey；METIS 補 systems/serving primary anchor，observability 與 privacy/access-control 仍薄 |

## 2. Core Survey Anchors — Keep This List Small

### General RAG
- **Gao et al. — Retrieval-Augmented Generation for Large Language Models: A Survey** (arXiv:2312.10997).  
  奠基性的 Naive / Advanced / Modular RAG 整理；保留作歷史 taxonomy anchor。  
  [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2023-12) Retrieval-Augmented Generation for Large Language Models - A Survey|Literature Note]]
- **Huang & Huang — A Survey on Retrieval-Augmented Text Generation for Large Language Models**, ACM Computing Surveys 58(12), Article 300, 2026, DOI: 10.1145/3805774 (arXiv:2404.10981).
  以資訊檢索視角整理 Pre-Retrieval / Retrieval / Post-Retrieval / Generation，補 general survey anchor。**已核內容是 2024-08-23 arXiv v2，37 頁；2026 期刊書目已核，38 頁正式全文尚未比對。** 本地 PDF 採正式版檔名，但內容仍為 v2。
  [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(ACM CSUR 2026-09) A Survey on Retrieval-Augmented Text Generation for Large Language Models|Literature Note：版本範圍與原文分類]]
- **Faridi et al. — Retrieval-Augmented Generation for Large Language Models: Evolution, Architectures, Applications, and Challenges (2020–2025)**, WIREs Data Mining and Knowledge Discovery, 2026, DOI: 10.1002/widm.70122.  
  作為目前較新的 broad survey anchor；涵蓋 retrieval granularity、indexing、reranking、context construction、retriever–generator integration、memory、agentic、GraphRAG、multimodal、evaluation 與 deployment risks。
- **Wu et al. — Retrieval-augmented generation for natural language processing: a survey**, Artificial Intelligence Review 59, 192 (2026), DOI: 10.1007/s10462-026-11605-7.  
  其中明確討論 RAG with knowledge-base update / index rebuild-or-update，可作 D10 的 survey-level support。

### Retrieval / Reasoning / Agentic
- **Li et al. — A Survey of RAG-Reasoning Systems in Large Language Models**, Findings of EMNLP 2025, DOI: 10.18653/v1/2025.findings-emnlp.648.  
  支撐 D05/D06/D12 的 multi-step reasoning ↔ retrieval 交互。
- **Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG** (2025).  
  支撐 D12 的 planning、tool use、reflection 與 multi-agent orchestration。  
  [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2025-01) Agentic Retrieval-Augmented Generation - A Survey on Agentic RAG|Literature Note]]

### Structured Knowledge / GraphRAG
- **Peng et al. — Graph Retrieval-Augmented Generation: A Survey**, ACM Transactions on Information Systems 44(2), 2026, DOI: 10.1145/3777378 (online first 2025-12-23).  
  以 Graph-Based Indexing → Graph-Guided Retrieval → Graph-Enhanced Generation 組織 GraphRAG；支撐 D03/D04/D05/D09 的 graph interface。  
  [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-08) Graph Retrieval-Augmented Generation - A Survey|Literature Note]]
- **Zhang et al. — A Survey of Generative Information Extraction**, COLING 2025.  
  支撐 D03 的 generative IE；**不**直接證明本 repo 的 information-preservation / F/R/D/A/P/C/T research proposal。

### Evaluation / Trustworthiness
- **Yu et al. — Evaluation of Retrieval-Augmented Generation: A Survey**, CCF BigData 2024 proceedings, Springer 2025, DOI: 10.1007/978-981-96-1024-2_8.  
  支撐 D13 的 retrieval / generation evaluation、faithfulness 與 benchmark design。  
  [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-05) Evaluation of Retrieval-Augmented Generation - A Survey|Literature Note]]
- **Ni et al. — Towards Trustworthy Retrieval Augmented Generation for Large Language Models: A Survey**, ACM Computing Surveys, 2026, DOI: 10.1145/3837074 (arXiv:2502.06872).  
  支撐 reliability、privacy、safety、fairness、explainability、accountability；主要對應 D14。
- **Khonde et al. — End-to-end security threats and defenses in retrieval-augmented LLM agents**, Discover Artificial Intelligence, 2026, DOI: 10.1007/s44163-026-01726-x.  
  最新 peer-reviewed security review 之一；明確整理 retrieval poisoning、indirect prompt injection、tool attacks 與跨 pipeline defenses。

### Memory / Persistent State
- **Memory in the Age of AI Agents** (arXiv:2512.13564).  
  這是 agent-memory survey，不是 RAG-only survey；它以 forms / functions / dynamics 整理 memory，適合支撐 D11 的 write / evolve / retrieve 邊界，但不能拿來宣稱 D11 是所有 RAG survey 的標準 top-level Domain。

### Adjacent but Important
- **Abootorabi et al. — Ask in Any Modality: A Comprehensive Survey on Multimodal Retrieval-Augmented Generation**, Findings of ACL 2025.  
  Multimodal 是 cross-cutting paradigm，不需要另建 top-level Domain。
- Long-context surveys 屬 **A01 Adjacent Interface**；用來比較 Long Context vs RAG，不應重新變成 RAG core Domain。

### Huang v2 → D01–D06：集中維護的 Coverage Crosswalk

此表只評估 **Huang 2024 arXiv v2 對各 Domain 的支撐強弱**，不代表全 repo 或整個社群的 survey coverage。D 編號與強弱判定是本 repo 的分析；原文是四階段分類（§2.2，pp. 4–5；Figure 3，p. 6），不是 D01–D14。頁碼均指已核的 v2 PDF。

| Repo Domain | v2 章節 / 頁碼 | 此篇的支撐強弱 | 分類邊界與仍需補的證據 |
|---|---|---|---|
| D01 Document Parsing & Structure Recovery | §2.1.1，p. 4；§3.3，p. 9 | **不足：coverage gap 保留** | text normalization／data augmentation 不能替代 OCR、layout、table、reading-order、結構恢復的專門 survey |
| D02 Segmentation & Retrieval Granularity | §2.1.1，p. 4；§2.2.1，pp. 4–5；§3.1，pp. 6–7 | **部分：基本定位** | 涉及句／段／文件粒度與階層索引，但不足以宣稱完整比較了 chunk-boundary、semantic-unit 或 granularity 的取捨 |
| D03 Knowledge Extraction & Consolidation | §3.3，p. 9；§4.1，pp. 10–11 | **間接：專門 coverage gap 保留** | data enrichment／利用既有 KG 不等於 entity / relation / event extraction、entity resolution 或 cross-chunk consolidation；§3.1 Graph 更不是 semantic KG extraction |
| D04 Representation & Indexing | §3.1，pp. 6–7 | **直接：broad indexing anchor** | Graph / PQ / LSH 是索引與 ANN 子題；向量鄰接圖和語義知識圖須分開。Embedding learning 細節仍回 primary paper |
| D05 Query Understanding & Retrieval | §3.2，pp. 7–8；§4.1，pp. 9–11；§5.1，pp. 15–16 | **直接：query / search / reranking anchor** | Query Manipulation 雖在 pre-retrieval、Re-Ranking 雖在 post-retrieval，依研究問題均可屬 D05；retriever-generator alignment 不宜只按階段定位 |
| D06 Evidence Sufficiency & Retrieval Control | §4.2，pp. 11–15；§5.2，pp. 16–17 | **直接支持 control；sufficiency 仍不足** | Conditional / Adaptive strategies 支持 retrieve / retry / stop；confidence、relevance filtering 不等於完整 evidence-set sufficiency，不能據此驗證 Idea 02 的 gap controller |

其他 Domain 的附帶導航：§5.2 中的 compression／context selection 可連 D07；§6 可連 D09；§7 評估連 D13。這些關聯不表示作者提出本 repo 的 hard boundaries。**Pre-Retrieval 也不是純粹的離線 corpus 建構階段**，它明確包括 query 側操作。

原文入口：[已核 v2 PDF](https://arxiv.org/pdf/2404.10981v2)；[v2 HTML](https://arxiv.org/html/2404.10981v2)。此表只用 survey 確認分類關聯；效果、演算法與研究建議仍須原始論文證據。

## 3. What Is Not Yet Survey-Backed Enough

下列內容可以保留為研究問題，但不要寫成「survey 已形成共識」：

- **D01 RAG-specific document parsing / structure recovery**：目前本頁的一般 RAG surveys 不能單靠 indexing／pre-retrieval 概述補足 parsing 專門 survey coverage；相關 primary parsing anchors 不代替 survey-level 核對。
- **D03 extraction / consolidation 的 RAG-specific 銜接**：已有 generative IE 與 GraphRAG survey 關聯；但不能把外部資料 enrichment、既有 KG retrieval 或 ANN graph 索引當作完整抽取與整合的證據。
- **D03 information-preserving extraction / extraction-to-RAG error propagation**：保留為 Level-2 research lens + Idea 01。
- **D06 explicit evidence requirement → gap localization → targeted retrieval controller**：現有 adaptive-retrieval literature 主要解 retrieval control，不等同完整 evidence-set sufficiency。
- **D08 provenance / governance arbitration**：RA-RAG 已直接支撐 source reliability；但 document lineage、Draft/Approved workflow、applicability scope 與多訊號聯合仲裁仍薄。
- **D10 production-grade continual index maintenance**：AURORA 已補 direct primary anchor，但 CRUD、deletion propagation、derived-index invalidation 與真實 update stream 仍缺。
- **D11 unified memory taxonomy**：interaction memory、model-side long-term memory、corpus/world memory 與 non-parametric continual knowledge 仍需用 memory survey / primary papers補齊。
- **D14 observability / privacy governance**：METIS 已補 RAG serving / scheduling，PoisonedRAG 補 corpus poisoning；仍缺 RAG-specific tracing/observability、ACL/tenant isolation 與 deletion/persistence governance。

## 4. Version / Deduplication Rule

1. 同一工作的 arXiv → conference/journal 原則上**保留一份 canonical note**，正式 venue / DOI 與已核全文版本分開記錄。版本同一性須核查，不因標題／作者相似就合併獨立擴充工作。
2. 正式版本可取得時，先比對章節、方法與實驗差異，再更新正文與本地 PDF；**正式全文無法取得時，保留已核的真實 preprint**，以 `source_version`／`verified_version`／核驗範圍標明，正式全文比對列待驗證。不可把舊全文標成已核最新正式版，也不可刪除唯一可查全文。
3. 舊 paper 若有獨立歷史或方法貢獻（例如 DPR、ColBERT、RAG 2020、FlashAttention）：**不因年份舊而刪除**。
4. Survey 不追求數量；每條研究軸保留 **1 個最新 broad anchor + 必要的專項 survey** 即可。
5. Comparative study、benchmark、method paper 不因標題像 survey 就放進本頁。

## 5. Verified Source Entrypoints

- General RAG (Gao): https://arxiv.org/abs/2312.10997
- General RAG (Huang & Huang): [arXiv 版本紀錄](https://arxiv.org/abs/2404.10981) · [已核 2024 v2](https://arxiv.org/pdf/2404.10981v2) · [2026 正式 DOI](https://doi.org/10.1145/3805774) · [正式書目登錄](https://api.crossref.org/works/10.1145/3805774)
- General RAG 2026 (Faridi et al.): https://doi.org/10.1002/widm.70122
- RAG for NLP Survey 2026 (Wu et al.): https://doi.org/10.1007/s10462-026-11605-7
- RAG-Reasoning Survey: https://aclanthology.org/2025.findings-emnlp.648/
- GraphRAG Survey: https://doi.org/10.1145/3777378
- Generative IE Survey: https://aclanthology.org/2025.coling-main.324/
- Multimodal RAG Survey: https://aclanthology.org/2025.findings-acl.861/
- RAG Evaluation Survey: https://doi.org/10.1007/978-981-96-1024-2_8
- Trustworthy RAG Survey: https://doi.org/10.1145/3837074
- End-to-end RAG Security Review 2026: https://doi.org/10.1007/s44163-026-01726-x
- Agent Memory Survey: https://arxiv.org/abs/2512.13564

> [!CAUTION]
> Survey 用來確認「研究線存在與如何被社群整理」；任何演算法流程、效果數字、速度、成本或 novelty claim 仍必須回 primary paper。
