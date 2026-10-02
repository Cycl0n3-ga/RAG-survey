---
title: "GraphRAG Literature Coverage Gaps — 2026-10-02"
tags:
  - literature-audit
  - graph-rag
  - reading-list
last_updated: "2026-10-02"
audit_mode: "parallel-subagents"
candidate_count: 44
independent_literature_notes_added: 4
candidate_status: "partial; 4 of 44 full-text notes added; 40 pending"
taxonomy_version: "v2"
---

# GraphRAG 文獻缺口與候選閱讀清單

查核日期：2026-10-02。範圍：本庫現有 177 篇 `paper_id` 筆記、129 個 `Papers/` PDF、全部 Markdown 的 title／alias／arXiv／DOI 提及。新增候選按識別碼與完整標題查重，共 **44 篇未見獨立筆記或 PDF**。查重盤點對照 [[03 - 論文庫 (Literature Notes)/README|Literature Notes]]；分類定義對照 [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Taxonomy & Domain Map]]。

**本頁是候選索引。** 初次盤點時共 44 篇候選；現已開始逐篇補全文與標準筆記：8/44 篇完成正式版全文核對、PDF 落檔與筆記建立（ToG、RoG、SubgraphRAG、GNN-RAG、PathRAG、HyperGraphRAG、OG-RAG、KGGen）；其餘候選仍待核對。下表的優先順序與 D01–D14 mapping 是本 repo 的補缺口建議；具體方法與實驗數據以各篇原始全文為準。

### 補齊進度

| 狀態 | 論文 | 筆記 |
|---|---|---|
| 已完成全文核對與 PDF | ToG — ICLR 2024 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph]] |
| 已完成全文核對與 PDF | RoG — ICLR 2024 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning]] |
| 已完成全文核對與 PDF | SubgraphRAG — ICLR 2025 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation]] |
| 已完成全文核對與 PDF | GNN-RAG — Findings ACL 2025 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs]] |
| 已完成全文核對與 PDF | PathRAG — AAAI 2026 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(AAAI 2026-03) PathRAG - Pruning Graph-Based Retrieval Augmented Generation with Relational Paths]] |
| 已完成全文核對與 PDF | HyperGraphRAG — NeurIPS 2025 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation]] |
| 已完成全文核對與 PDF | OG-RAG — EMNLP 2025 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models]] |
| 已完成全文核對與 PDF | KGGen — NeurIPS 2025 | [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models]] |
| 待完成 | 其他 36 篇 | 正式 PDF 與筆記尚未補齊 |

## 目錄

- [收錄狀態與優先順序](#coverage-and-priority)
- [圖檢索與知識圖譜推理](#graph-retrieval)
  - [ToG](#paper-sun2023-thinkongraph)
  - [ToG-2](#paper-ma2024-thinkongraph2)
  - [RoG](#paper-luo2023-reasoningongraphs)
  - [SubgraphRAG](#paper-li2024-subgraphrag)
  - [GNN-RAG](#paper-gnn-rag)
  - [GRAG](#paper-grag)
  - [KG-FiD](#paper-kg-fid)
  - [G-RAG](#paper-dong2024-grag-reranking)
  - [FastToG](#paper-liang2025-fastthinkongraph)
  - [PoG](#paper-tan2024-pathsovergraph)
  - [SimGRAG](#paper-cai2024-simgrag)
  - [PathRAG](#paper-chen2025-pathrag)
  - [CatRAG（Traversal）](#paper-catrag-traversal)
  - [DynaGRAG](#paper-thakrar2024-dynagrag)
- [圖建構、超圖與結構表示](#graph-structure)
  - [HyperGraphRAG](#paper-luo2025-hypergraphrag)
  - [HyperRAG（n-ary）](#paper-lien2026-hyperrag-nary)
  - [OG-RAG](#paper-og-rag)
  - [HyperRAG（Hyperbolic）](#paper-hyperrag-hyperbolic)
  - [ReGraphRAG](#paper-kim2025-regraphrag)
  - [KGGen](#paper-mo2025-kggen)
  - [MeshRAG](#paper-meshrag)
- [證據控制、圖式記憶與編排](#graph-control-memory)
  - [A2RAG](#paper-a2rag)
  - [StructRAG](#paper-li2024-structrag)
  - [Zep／Graphiti](#paper-rasmussen2025-zep)
  - [DyG-RAG](#paper-sun2025-dygrag)
  - [KAG](#paper-liang2024-kag)
  - [StructGPT](#paper-jiang2023-structgpt)
  - [HybGRAG](#paper-lee2024-hybgrag)
  - [GeAR](#paper-shen2024-gear)
  - [HydraRAG](#paper-tan2025-hydrarag)
- [評測、比較研究、Survey 與安全](#graph-evaluation-security)
  - [GraphRAG-Bench 論文](#paper-xiang2025-graphragbench)
  - [WildGraphBench](#paper-wang2026-wildgraphbench)
  - [Graph-CoT／GRBench](#paper-jin2024-graphcot)
  - [PVLDB Unified Analysis](#paper-zhou2025-graphragunifiedanalysis)
  - [Han et al. GraphRAG Survey](#paper-han2024-graphragsurvey)
  - [QO-Bench](#paper-zhang2026-qobench)
  - [GRADA](#paper-zheng2025-grada)
  - [LogicPoison](#paper-xiao2026-logicpoison)
- [抽取支援與非圖式基線](#enabling-baselines)
  - [Re-DocRED](#paper-tan2022-redocred)
  - [GLiNER](#paper-zaratiana2023-gliner)
  - [FiD](#paper-fid)
  - [M3-Embedding／BGE-M3](#paper-m3-embedding)
  - [UPR](#paper-upr)
  - [Nougat](#paper-nougat)
- [分類與版本邊界](#taxonomy-version-boundaries)
- [查核方式與限制](#checks-and-limits)

<a id="coverage-and-priority"></a>
## 收錄狀態與優先順序

「未見獨立筆記／PDF」與「完全沒有提過」需分開。**GraphRAG-Bench** 已在 LinearRAG 的 benchmark 與正文出現；**FiD** 在 Atlas 正文出現；**M3-Embedding／BGE-M3** 已列 D04 候選並出現在多篇筆記；**Nougat** 已列 D01 候選。其他 40 項未找到實質正文提及。這是 2026-10-02 的檔案及文字查核結果，非宣稱已窮盡所有 PDF 的 references。

目前已有 GraphRAG、LightRAG、HippoRAG 1／2、GFM-RAG、KG2RAG、GraphReader、PropRAG、LinearRAG、RAPTOR、CrossAug。它們仍是比較的既有 anchor，本頁不重複列為新增；收錄位置見 [[03 - 論文庫 (Literature Notes)/README|Literature Notes Index]]。

第一批建議讀下列 **16 篇**，依補足不同機制與評測缺口排序。效能選型仍需回到同條件實驗。

| 候選與已核版本 | 先補的問題 | 建議主領域 |
|---|---|---|
| [ToG](https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html) — ICLR 2024 | LLM 引導 KG beam search | D05 |
| [RoG](https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html) — ICLR 2024 | relation-path planning | D05 |
| [SubgraphRAG](https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html) — ICLR 2025 | 可學習的子圖選擇 | D05 |
| [GNN-RAG](https://aclanthology.org/2025.findings-acl.856/) — Findings ACL 2025 | GNN 候選與最短路徑 | D05 |
| [PathRAG](https://ojs.aaai.org/index.php/AAAI/article/view/40268) — AAAI 2026 | relational-path pruning | D05 |
| [HyperGraphRAG](https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html) — NeurIPS 2025 | n-ary facts 的超圖表示 | D04 |
| [OG-RAG](https://aclanthology.org/2025.emnlp-main.1674/) — EMNLP 2025 | ontology-grounded hypergraph | D04 |
| [KGGen](https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html) — NeurIPS 2025 | 實體／關係抽取與整併 | D03 |
| [StructRAG](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html) — ICLR 2025 | task-conditioned context structuring | D07 |
| [A2RAG](https://arxiv.org/abs/2601.21162) — arXiv 2026 | sufficiency 與 targeted refinement | D06 |
| [Zep／Graphiti](https://arxiv.org/abs/2501.13956) — arXiv 2025 | bi-temporal graph memory | D11 |
| [CatRAG（Traversal）](https://aclanthology.org/2026.findings-acl.290/) — Findings ACL 2026 | query-aware PPR 與完整證據鏈 | D05 |
| [GraphRAG-Bench 論文](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html) — ICLR 2026 | 建圖→檢索→生成的任務評測 | D13 |
| [WildGraphBench](https://aclanthology.org/2026.findings-acl.679/) — Findings ACL 2026 | 異質外部長文件評測 | D13 |
| [PVLDB Unified Analysis](https://www.vldb.org/pvldb/vol18/p5623-zhou.pdf) — PVLDB 2025 | 共同設定與組件分析 | D13 |
| [LogicPoison](https://aclanthology.org/2026.acl-long.252/) — ACL 2026 | graph-topology 攻擊 | D14 |

<a id="graph-retrieval"></a>
## 圖檢索與知識圖譜推理

| 候選與已核版本 | 補缺口軸 | 建議主／次領域 | 優先級 |
|---|---|---|---|
| [ToG](https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html) — ICLR 2024 | LLM 引導 KG beam search | D05／D12 | P1 |
| [ToG-2](https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html) — ICLR 2025 | KG 與文件交替檢索 | D05／D04 | P2 |
| [RoG](https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html) — ICLR 2024 | relation-path planning | D05／D09 | P1 |
| [SubgraphRAG](https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html) — ICLR 2025 | 可學習的子圖選擇 | D05 | P1 |
| [GNN-RAG](https://aclanthology.org/2025.findings-acl.856/) — Findings ACL 2025 | GNN 候選與最短路徑 | D05／D04／D07 | P1 |
| [GRAG](https://aclanthology.org/2025.findings-naacl.232/) — Findings NAACL 2025 | textual subgraphs 與拓撲 | D05／D04／D07 | P2 |
| [KG-FiD](https://aclanthology.org/2022.acl-long.340/) — ACL 2022 | KG 引導 passages reranking | D05／D04／D07 | P2 |
| [G-RAG](https://arxiv.org/abs/2405.18414) — arXiv 2024 | 跨文件／AMR graph reranking | D05 | P2 |
| [FastToG](https://arxiv.org/abs/2501.14300) — arXiv 2025 | community 作為搜尋單位 | D05／D07 | P2 |
| [PoG](https://arxiv.org/abs/2410.14211) — WWW 2025 | 多實體問題的路徑探索 | D05 | P2 |
| [SimGRAG](https://aclanthology.org/2025.findings-acl.163/) — Findings ACL 2025 | query-to-pattern 子圖匹配 | D05 | P2 |
| [PathRAG](https://ojs.aaai.org/index.php/AAAI/article/view/40268) — AAAI 2026 | relational-path pruning | D05／D07 | P1 |
| [CatRAG（Traversal）](https://aclanthology.org/2026.findings-acl.290/) — Findings ACL 2026 | query-aware PPR 與完整證據鏈 | D05／D04／D13 | P1 |
| [DynaGRAG](https://arxiv.org/abs/2412.18644) — arXiv 2024 | query-aware subgraph BFS | D05／D04 | P2 |

P1 為上表第一批；P2 為後續按研究問題選讀。分類與優先級均待全文核對後定案。

<a id="paper-sun2023-thinkongraph"></a>
### ToG

**完整標題：** [Think-on-Graph: Deep and Responsible Reasoning of Large Language Model on Knowledge Graph](https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html)。

**作者（本次核對版本）：** Jiashuo Sun；Chengjin Xu；Lumingyuan Tang；Saizhuo Wang；Chen Lin；Yeyun Gong；Lionel M. Ni；Heung-Yeung Shum；Jian Guo。

**書目：** 預印年份：2023；正式出版年份：2024；已核 venue／狀態：ICLR 2024。

**識別碼：** [arXiv:2307.07697](https://arxiv.org/abs/2307.07697)。

**內容與補缺分析：** 機制：讓 LLM agent 在 KG 上反覆執行 beam search、探索 entities/relations，依檢索知識推理。補缺判斷：可補本庫 associative retrieval 之外的 LLM-guided KG traversal，並與 GraphReader 的文件圖探索分開比較。Domain mapping 為本次分析建議，非作者分類。 [原始來源：ToG, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D12。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；未核方法全文或實驗；arXiv 的 Lionel M. Ni 與正式 proceedings 的 Lionel Ni 名稱呈現不同，不代表不同作者。

**核對位置：** [metadata、Abstract、Submission history v1 (2023-07-15)](https://arxiv.org/abs/2307.07697)：預印年份、完整作者名單、搜尋機制；[title、authors、ICLR 2024 Conference、Abstract](https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html)：正式版本與 venue/year。

<a id="paper-ma2024-thinkongraph2"></a>
### ToG-2

**完整標題：** [Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation](https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html)。

**作者（本次核對版本）：** Shengjie Ma；Chengjin Xu；Xuhui Jiang；Muzhi Li；Huaren Qu；Cehao Yang；Jiaxin Mao；Jian Guo。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：ICLR 2025。

**識別碼：** [arXiv:2407.10805](https://arxiv.org/abs/2407.10805)。

**內容與補缺分析：** 機制：KG 透過 entities 連接 documents，引導 context retrieval；documents 又作為 entity contexts 改善 graph retrieval，兩者反覆交替。補缺判斷：可補 KG×text 的互相約束機制，與單純融合多個 retrieval channels 或單向 KG-guided chunk expansion 對照。Domain mapping 為本次分析建議。 [原始來源：ToG-2, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；未查驗停止條件、全文機制細節、實驗數據或與初版的完整差異。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-07-15)](https://arxiv.org/abs/2407.10805)：預印年份、作者與機制；[title、authors、ICLR 2025 Conference、Abstract](https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html)：正式版本、venue/year與 tight coupling。

<a id="paper-luo2023-reasoningongraphs"></a>
### RoG

**完整標題：** [Reasoning on Graphs: Faithful and Interpretable Large Language Model Reasoning](https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html)。

**作者（本次核對版本）：** Linhao Luo；Yuan-Fang Li；Gholamreza Haffari；Shirui Pan。

**書目：** 預印年份：2023；正式出版年份：2024；已核 venue／狀態：ICLR 2024。

**識別碼：** [arXiv:2310.01061](https://arxiv.org/abs/2310.01061)。

**內容與補缺分析：** 機制：planning–retrieval–reasoning；先生成 KG-grounded relation-path plans，再檢索有效 reasoning paths，並以 KG 知識蒸餾訓練推理能力。補缺判斷：可補 relation-path planning 與 graph-specific training signal，和無訓練的 ToG 搜尋、PropRAG proposition-path retrieval 分開比較。Domain mapping 為本次分析建議。 [原始來源：RoG, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；PDF 僅核 title page / Abstract；未讀訓練公式、path validity條件或實驗全文。

**核對位置：** [metadata、Abstract、Submission history v1 (2023-10-02)](https://arxiv.org/abs/2310.01061)：預印年份、完整作者與機制；[ICLR 2024 Conference、Abstract](https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html)：正式 venue/year；該頁作者名呈現 Reza Haffari；[PDF title page / Abstract](https://openreview.net/pdf?id=ZGNWW7xZ6Q)：正式 PDF 呈現 Gholamreza Haffari。

<a id="paper-li2024-subgraphrag"></a>
### SubgraphRAG

**完整標題：** [Simple is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation](https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html)。

**作者（本次核對版本）：** Mufei Li；Siqi Miao；Pan Li。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：ICLR 2025。

**識別碼：** [arXiv:2410.20724](https://arxiv.org/abs/2410.20724)。

**內容與補缺分析：** 機制：SubgraphRAG 以輕量 MLP、parallel triple scoring 和 directional structural distances 檢索子圖；子圖大小可隨 query 需求及 downstream LLM 能力調整。補缺判斷：可補 learned triple/subgraph scoring 與 retrieval budget 的機制軸，避免 graph retrieval 只介紹 LLM 搜尋或 PPR。Domain mapping 為本次分析建議。 [原始來源：SubgraphRAG, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；未查驗 retriever labels、budget selection、training 或實驗全文；arXiv title 的 Is 大寫、proceedings 的 is 小寫。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-10-28)](https://arxiv.org/abs/2410.20724)：預印年份、作者；[title、authors、ICLR 2025 Conference、Abstract](https://proceedings.iclr.cc/paper_files/paper/2025/hash/11e1900e680f5fe1893a8e27362dbe2c-Abstract-Conference.html)：正式版本、venue/year與 MLP retrieval。

<a id="paper-gnn-rag"></a>
### GNN-RAG

**完整標題：** [GNN-RAG: Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs](https://aclanthology.org/2025.findings-acl.856/)。

**作者（本次核對版本）：** Costas Mavromatis；George Karypis。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：Findings of ACL 2025。

**識別碼：** [arXiv:2405.20139](https://arxiv.org/abs/2405.20139)；[DOI: 10.18653/v1/2025.findings-acl.856](https://doi.org/10.18653/v1/2025.findings-acl.856)。

**內容與補缺分析：** GNN 找出問題相關候選節點，再取連接問題實體與候選的最短路徑供 LLM 使用。 [原始來源：GNN-RAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.findings-acl.856/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04, D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** 關聯預印本標題較短；本清單採正式版本標題，尚未逐章比對版本差異。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-grag"></a>
### GRAG

**完整標題：** [GRAG: Graph Retrieval-Augmented Generation](https://aclanthology.org/2025.findings-naacl.232/)。

**作者（本次核對版本）：** Yuntong Hu；Zhihan Lei；Zheng Zhang；Bo Pan；Chen Ling；Liang Zhao。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：Findings of NAACL 2025。

**識別碼：** [arXiv:2405.16506](https://arxiv.org/abs/2405.16506)；[DOI: 10.18653/v1/2025.findings-naacl.232](https://doi.org/10.18653/v1/2025.findings-naacl.232)。

**內容與補缺分析：** 檢索 textual subgraphs，並結合 text view 與 graph view 向生成模型提供文字與拓撲資訊。 [原始來源：GRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.findings-naacl.232/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04, D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-kg-fid"></a>
### KG-FiD

**完整標題：** [KG-FiD: Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering](https://aclanthology.org/2022.acl-long.340/)。

**作者（本次核對版本）：** Donghan Yu；Chenguang Zhu；Yuwei Fang；Wenhao Yu；Shuohang Wang；Yichong Xu；Xiang Ren；Yiming Yang；Michael Zeng。

**書目：** 預印年份：2021；正式出版年份：2022；已核 venue／狀態：ACL 2022。

**識別碼：** [arXiv:2110.04330](https://arxiv.org/abs/2110.04330)；[DOI: 10.18653/v1/2022.acl-long.340](https://doi.org/10.18653/v1/2022.acl-long.340)。

**內容與補缺分析：** 用 KG 建立已檢索 passages 間的結構關係，再用 GNN reranking 篩選 reader 的輸入。 [原始來源：KG-FiD, Abstract／詳見閱讀範圍](https://aclanthology.org/2022.acl-long.340/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04, D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-dong2024-grag-reranking"></a>
### G-RAG

**完整標題：** [Don't Forget to Connect! Improving RAG with Graph-based Reranking](https://arxiv.org/abs/2405.18414)。

**作者（本次核對版本）：** Jialin Dong；Bahare Fatemi；Bryan Perozzi；Lin F. Yang；Anton Tsitsulin。

**書目：** 預印年份：2024；正式出版年份：未核得正式記錄；已核 venue／狀態：2024 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2405.18414](https://arxiv.org/abs/2405.18414)；[arXiv-issued DOI（不是正式會議 DOI）: 10.48550/arXiv.2405.18414](https://doi.org/10.48550/arXiv.2405.18414)。

**內容與補缺分析：** 機制：G-RAG 是 retriever 與 reader 之間的 GNN reranker，結合跨文件 connections 與 Abstract Meaning Representation graphs 的語意資訊。補缺判斷：可補 graph-aware reranking，明確區分 graph 用於索引／first-stage search 與 graph 用於候選相關性排序。Domain mapping 為本次分析建議；勿與 Hu et al. 的 GRAG 混名。 [原始來源：G-RAG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2405.18414)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；doi 為 arXiv DOI，不代表正式會議 DOI；未核正式出版版本、全文或實驗數字。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-05-28)、arXiv-issued DOI](https://arxiv.org/abs/2405.18414)：標題、完整作者、預印年份、AMR/GNN reranking。

<a id="paper-liang2025-fastthinkongraph"></a>
### FastToG

**完整標題：** [Fast Think-on-Graph: Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph](https://arxiv.org/abs/2501.14300)。

**作者（本次核對版本）：** Xujian Liang；Zhaoquan Gu。

**書目：** 預印年份：2025；正式出版年份：未核得正式記錄；已核 venue／狀態：2025 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2501.14300](https://arxiv.org/abs/2501.14300)；[arXiv-issued DOI（不是正式會議 DOI）: 10.48550/arXiv.2501.14300](https://doi.org/10.48550/arXiv.2501.14300)。

**內容與補缺分析：** 機制：FastToG 以 community-by-community 搜尋，利用 community detection、coarse/fine 兩階段 pruning，並將 community graph 轉為文本。補缺判斷：可補 community 作為 query-time search unit 的研究，而非僅 corpus-side community summary indexing；亦可比較 retrieval與 graph-to-text context 的介面。Domain mapping 為本次分析建議。 [原始來源：FastToG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2501.14300)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；doi 為 arXiv DOI；未核正式版本或效率比較的硬體、成本與實驗條件。

**核對位置：** [metadata、Abstract、Submission history v1 (2025-01-24)、arXiv-issued DOI](https://arxiv.org/abs/2501.14300)：完整作者、預印年份、community pruning / Community-to-Text。

<a id="paper-tan2024-pathsovergraph"></a>
### PoG

**完整標題：** [Paths-over-Graph: Knowledge Graph Empowered Large Language Model Reasoning](https://arxiv.org/abs/2410.14211)。

**作者（本次核對版本）：** Xingyu Tan；Xiaoyang Wang；Qing Liu；Xiwei Xu；Xin Yuan；Wenjie Zhang。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：The Web Conference 2025 (WWW 2025)。

**識別碼：** [arXiv:2410.14211](https://arxiv.org/abs/2410.14211)；[DOI: 10.1145/3696410.3714892](https://doi.org/10.1145/3696410.3714892)。

**內容與補缺分析：** 機制：PoG 處理 multi-hop / multi-entity questions，以動態路徑探索及 graph structure、LLM prompting、預訓練語言模型三類 pruning 縮小候選路徑。補缺判斷：可補多 topic entities 的 path constraints，與 entity-seed PPR、single-path planning 與 proposition-path retrieval 比較。Domain mapping 為本次分析建議。 [原始來源：PoG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2410.14211)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_arxiv_metadata_and_abstract_only；正式 venue/year/DOI 另核 ACM 向 Crossref 登錄的原始出版 metadata；ACM 正式全文未取得，未比對版本差異或數字。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-10-18)](https://arxiv.org/abs/2410.14211)：完整作者、預印年份與 mechanism；[ACM publisher-deposited metadata：title、authors、publisher、container-title、published 2025-04-22、DOI、pp.3505–3522](https://api.crossref.org/works/10.1145/3696410.3714892)：正式出版 metadata；ACM landing page 403，未核正式 PDF全文；[publisher landing page](https://dl.acm.org/doi/10.1145/3696410.3714892)：正式版連結；本次存取 403。

<a id="paper-cai2024-simgrag"></a>
### SimGRAG

**完整標題：** [SimGRAG: Leveraging Similar Subgraphs for Knowledge Graphs Driven Retrieval-Augmented Generation](https://aclanthology.org/2025.findings-acl.163/)。

**作者（本次核對版本）：** Yuzheng Cai；Zhenyue Guo；Yiwen Pei；Wanrui Bian；Weiguo Zheng。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：Findings of ACL 2025。

**識別碼：** [arXiv:2412.15272](https://arxiv.org/abs/2412.15272)；[DOI: 10.18653/v1/2025.findings-acl.163](https://doi.org/10.18653/v1/2025.findings-acl.163)。

**內容與補缺分析：** 機制：query-to-pattern 將自然語言需求變成 graph pattern；pattern-to-subgraph 再用 graph semantic distance 比較並檢索相似子圖。補缺判斷：可補 query text 與 KG structure 的對齊，以及 pattern-based graph matching，與 embedding similarity、PPR 或 beam traversal 分開比較。Domain mapping 為本次分析建議。 [原始來源：SimGRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.findings-acl.163/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；PDF 僅核 title page / Abstract；未讀 GSD 定義、search algorithm 或實驗全文。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-12-17)](https://arxiv.org/abs/2412.15272)：預印年份與作者；[metadata、Abstract、DOI；pp.3139–3158](https://aclanthology.org/2025.findings-acl.163/)：正式 Findings ACL 2025、query-to-pattern / pattern-to-subgraph；作者欄呈現 YiWen / WanRui；[PDF title page / Abstract](https://aclanthology.org/2025.findings-acl.163.pdf)：PDF 作者呈現 Yiwen Pei / Wanrui Bian。

<a id="paper-chen2025-pathrag"></a>
### PathRAG

**完整標題：** [PathRAG: Pruning Graph-based Retrieval Augmented Generation with Relational Paths](https://ojs.aaai.org/index.php/AAAI/article/view/40268)。

**作者（本次核對版本）：** Boyu Chen；Zirui Guo；Zidan Yang；Yuluo Chen；Junze Chen；Zhenghao Liu；Chuan Shi；Cheng Yang。

**書目：** 預印年份：2025；正式出版年份：2026；已核 venue／狀態：AAAI 2026 (Proceedings of the AAAI Conference on Artificial Intelligence 40(36))。

**識別碼：** [arXiv:2502.14902](https://arxiv.org/abs/2502.14902)；[DOI: 10.1609/aaai.v40i36.40268](https://doi.org/10.1609/aaai.v40i36.40268)。

**內容與補缺分析：** 原文機制：从 indexing graph 擷取 relational paths，以 flow-based pruning 降低所取資訊冗餘，再轉寫 paths 組成 prompting context。補缺口判斷（本 repo 建議）：補 D05 的 path 作為 retrieval unit、D07 的路徑序列化；不把作者針對所測方法的 redundancy diagnosis 推廣為所有 GraphRAG 的主要失效原因。 [原始來源：PathRAG, Abstract／詳見閱讀範圍](https://ojs.aaai.org/index.php/AAAI/article/view/40268)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀正式官方摘要及 publication metadata；全文方法細節與實驗待查驗。

**核對位置：** AAAI2026 official article Abstract/title/all8authors/DOI/published2026-03-14；arXiv2502.14902 submission history（2025preprint）。。

<a id="paper-catrag-traversal"></a>
### CatRAG（Traversal）

**完整標題：** [Breaking the Static Graph: Context-Aware Traversal for Graph-Based RAG](https://aclanthology.org/2026.findings-acl.290/)。

**作者（本次核對版本）：** Kwun Hang Lau；Fangyuan Zhang；Boyu Ruan；Yingli Zhou；Qintian Guo；Ruiyuan Zhang；Xiaofang Zhou。

**書目：** 預印年份：2026；正式出版年份：2026；已核 venue／狀態：Findings of ACL 2026。

**識別碼：** [arXiv:2602.01965](https://arxiv.org/abs/2602.01965)；[DOI: 10.18653/v1/2026.findings-acl.290](https://doi.org/10.18653/v1/2026.findings-acl.290)。

**內容與補缺分析：** 在 HippoRAG 2 上加入 query-aware edge weighting、symbolic anchoring 與 key-fact passage bias，以改善多跳證據鏈召回。 [原始來源：CatRAG（Traversal）, Abstract／詳見閱讀範圍](https://aclanthology.org/2026.findings-acl.290/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04, D13。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** 與 arXiv:2603.21524 的 CatRAG Debiasing 是不同工作；摘要中的 reasoning completeness 不等於 D06 的 retrieve/retry/stop controller。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-thakrar2024-dynagrag"></a>
### DynaGRAG

**完整標題：** [DynaGRAG | Exploring the Topology of Information for Advancing Language Understanding and Generation in Graph Retrieval-Augmented Generation](https://arxiv.org/abs/2412.18644)。

**作者（本次核對版本）：** Karishma Thakrar。

**書目：** 預印年份：2024；正式出版年份：未核得正式記錄；已核 venue／狀態：2024 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2412.18644](https://arxiv.org/abs/2412.18644)。

**內容與補缺分析：** 原文機制：結合 deduplication、two-step mean pooling、query-aware unique-node retrieval 與 Dynamic Similarity-Aware BFS，以檢索並組織相關且多樣的 subgraphs。補缺口判斷（本 repo 建議）：作為 D05 query-aware graph traversal / D04 subgraph representation 的探索候選；摘要中的 dynamic 指檢索優先次序與遍歷，不足以認定具有 D10 的來源同步或時間版本維護。 [原始來源：DynaGRAG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2412.18644)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 僅基於官方摘要整理，全文待查驗；正式出版未核實。

**版本注意：** 較早索引題名為 DynaGRAG: Improving Language Understanding and Generation through Dynamic Subgraph Representation in Graph Retrieval-Augmented Generation；本條採官方現行題名，不另算一篇。

**核對位置：** arXiv2412.18644v3 Abstract/title/authors/submission history。。

<a id="graph-structure"></a>
## 圖建構、超圖與結構表示

| 候選與已核版本 | 補缺口軸 | 建議主／次領域 | 優先級 |
|---|---|---|---|
| [HyperGraphRAG](https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html) — NeurIPS 2025 | n-ary facts 的超圖表示 | D04／D03／D05 | P1 |
| [HyperRAG（n-ary）](https://arxiv.org/abs/2602.14470) — WWW 2026 | 超圖 traversal 與推理鏈 | D05／D04 | P2 |
| [OG-RAG](https://aclanthology.org/2025.emnlp-main.1674/) — EMNLP 2025 | ontology-grounded hypergraph | D04／D05／D07 | P1 |
| [HyperRAG（Hyperbolic）](https://aclanthology.org/2026.acl-long.986/) — ACL 2026 | 雙曲空間與 query-aware graph | D05／D04 | P2 |
| [ReGraphRAG](https://aclanthology.org/2025.findings-emnlp.290/) — Findings EMNLP 2025 | 碎裂圖重組與多視角 | D04／D03／D05 | P2 |
| [KGGen](https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html) — NeurIPS 2025 | 實體／關係抽取與整併 | D03／D04 | P1 |
| [MeshRAG](https://aclanthology.org/2026.acl-long.1156/) — ACL 2026 | hash-induced graph construction | D04／D05／D14 | P2 |

P1 為上表第一批；P2 為後續按研究問題選讀。分類與優先級均待全文核對後定案。

<a id="paper-luo2025-hypergraphrag"></a>
### HyperGraphRAG

**完整標題：** [HyperGraphRAG: Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation](https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html)。

**作者（本次核對版本）：** Haoran Luo；Haihong E；Guanting Chen；Yandan Zheng；Xiaobao Wu；Yikai Guo；Qika Lin；Yu Feng；Zemin Kuang；Meina Song；Yifan Zhu；Luu Anh Tuan。

**書目：** 預印年份：2025；正式出版年份：2025；已核 venue／狀態：NeurIPS 2025 main conference。

**識別碼：** [arXiv:2503.21322](https://arxiv.org/abs/2503.21322)；[DOI: 10.52202/085713-5089](https://doi.org/10.52202/085713-5089)。

**內容與補缺分析：** 原文機制：以 hyperedge 表示 n-ary relational facts，串接知識超圖建構、檢索與生成。補缺口判斷（本 repo 建議）：可補 D04 的高階關係表示與 D03→D04 圖建構接口，避免把 GraphRAG 全等同於二元實體關係圖；不由摘要推導所有既有圖方法皆無法表達多元事實。 [原始來源：HyperGraphRAG, Abstract／詳見閱讀範圍](https://proceedings.neurips.cc/paper_files/paper/2025/hash/df55ee6e59f8ac4a625219e11fe9ddba-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D04；secondary_domains = D03, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀官方摘要與出版 metadata；全文機制與實驗待查驗。

**版本注意：** 正式 proceedings landing page 最末作者列 Anh Tuan Luu，arXiv/PDF 列 Luu Anh Tuan；authors 此處採 arXiv/PDF 姓名形式。

**核對位置：** NeurIPS 2025 官方 Abstract / title / author list / DOI；arXiv2503.21322 submission history。。

<a id="paper-lien2026-hyperrag-nary"></a>
### HyperRAG（n-ary）

**完整標題：** [HyperRAG: Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation](https://arxiv.org/abs/2602.14470)。

**作者（本次核對版本）：** Wen-Sheng Lien；Yu-Kai Chan；Hao-Lung Hsiao；Bo-Kai Ruan；Meng-Fen Chiang；Chien-An Chen；Yi-Ren Yeh；Hong-Han Shuai。

**書目：** 預印年份：2026；正式出版年份：2026；已核 venue／狀態：Proceedings of the ACM Web Conference 2026 (WWW 2026)。

**識別碼：** [arXiv:2602.14470](https://arxiv.org/abs/2602.14470)；[DOI: 10.1145/3774904.3792710](https://doi.org/10.1145/3774904.3792710)。

**內容與補缺分析：** 原文機制：HyperRetriever 學習 structural-semantic n-ary fact traversal，形成 query-conditioned chains；HyperMemory 以 LLM parametric memory 引導 beam-search 路徑擴展。補缺口判斷（本 repo 建議）：補 D05 的高階關係 traversal，與 HyperGraphRAG 的表示建構分開；HyperMemory 並非本文所定義的持續外部記憶，因此不因名稱歸 D11。 [原始來源：HyperRAG（n-ary）, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2602.14470)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀官方摘要與 arXiv metadata；已核 ACM Crossref deposit，正式版全文待查驗。

**版本注意：** 不要與 ACL2026 Chuang Zhou 等 Query-Aware Knowledge Retrieval via Hyperbolic Structuring（其方法也叫 HyperRAG）或 Hyper-RAG2504.08758 混為同一研究。

**核對位置：** arXiv2602.14470v1 Abstract / authors / WWW2026 acceptance / related DOI；ACM DOI registration metadata: https://api.crossref.org/works/10.1145/3774904.3792710 (publisher-deposited title/authors/venue/year)。。

<a id="paper-og-rag"></a>
### OG-RAG

**完整標題：** [OG-RAG: Ontology-grounded retrieval-augmented generation for large language models](https://aclanthology.org/2025.emnlp-main.1674/)。

**作者（本次核對版本）：** Kartik Sharma；Peeyush Kumar；Yunqing Li。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：EMNLP 2025。

**識別碼：** [arXiv:2412.15235](https://arxiv.org/abs/2412.15235)；[DOI: 10.18653/v1/2025.emnlp-main.1674](https://doi.org/10.18653/v1/2025.emnlp-main.1674)。

**內容與補缺分析：** 以 domain ontology 建構知識超圖，再透過最佳化挑選 query 所需的超邊集合。 [原始來源：OG-RAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.emnlp-main.1674/)。

**建議定位：** 方法論文；primary_domain = D04；secondary_domains = D05, D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-hyperrag-hyperbolic"></a>
### HyperRAG（Hyperbolic）

**完整標題：** [Query-Aware Knowledge Retrieval via Hyperbolic Structuring](https://aclanthology.org/2026.acl-long.986/)。

**作者（本次核對版本）：** Chuang Zhou；Junnan Dong；Yilin Xiao；Shengyuan Chen；Su Dong；di Yin；Xing Sun；Zhaozhuo Xu；Xiao Huang。

**書目：** 預印年份：未核得；正式出版年份：2026；已核 venue／狀態：ACL 2026。

**識別碼：** [DOI: 10.18653/v1/2026.acl-long.986](https://doi.org/10.18653/v1/2026.acl-long.986)。

**內容與補缺分析：** HyperRAG 在雙曲空間結合 entity-based links 與隱含 query-aware connections，建立查詢導向圖結構。 [原始來源：HyperRAG（Hyperbolic）, Abstract／詳見閱讀範圍](https://aclanthology.org/2026.acl-long.986/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** 與 Lien 等人的 n-ary hypergraph HyperRAG 不同；本次未核得關聯 arXiv ID，預印年份留空。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-kim2025-regraphrag"></a>
### ReGraphRAG

**完整標題：** [ReGraphRAG: Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation](https://aclanthology.org/2025.findings-emnlp.290/)。

**作者（本次核對版本）：** Soohyeong Kim；Seok Jun Hwang；JungHyoun Kim；Jeonghyeon Park；Yong Suk Choi。

**書目：** 預印年份：未核得；正式出版年份：2025；已核 venue／狀態：Findings of the Association for Computational Linguistics: EMNLP 2025。

**識別碼：** [DOI: 10.18653/v1/2025.findings-emnlp.290](https://doi.org/10.18653/v1/2025.findings-emnlp.290)。

**內容與補缺分析：** 原文機制：針對從文件抽取後碎裂的 knowledge graphs，組合 Graph Reorganization、Perspective Expansion 與 Query-aware Reranking。補缺口判斷（本 repo 建議）：補 D04 圖連通性與組織、D03→D04 consolidation 接口和 D05 query-aware re-ranking；新增連接與 perspective expansion 的來源忠實度須在全文核對，不能由摘要推定它們皆由原文直接支持。 [原始來源：ReGraphRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.findings-emnlp.290/)。

**建議定位：** 方法論文；primary_domain = D04；secondary_domains = D03, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 僅基於官方摘要整理，全文待查驗；未找到可核 preprint identifier，因此preprint_year/arxiv留null。

**核對位置：** ACL Anthology2025.findings-emnlp.290 Abstract、完整5authors、FindingsEMNLP2025年份與DOI。。

<a id="paper-mo2025-kggen"></a>
### KGGen

**完整標題：** [KGGen: Extracting Knowledge Graphs from Plain Text with Language Models](https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html)。

**作者（本次核對版本）：** Belinda Mo；Kyssen Yu；Joshua Kazdan；Joan Cabezas；Proud Mpala；Lisa Yu；Chris Cundy；Charilaos Kanatsoulis；Sanmi Koyejo。

**書目：** 預印年份：2025；正式出版年份：2025；已核 venue／狀態：NeurIPS 2025 main conference。

**識別碼：** [arXiv:2502.09956](https://arxiv.org/abs/2502.09956)；[DOI: 10.52202/085713-1010](https://doi.org/10.52202/085713-1010)。

**內容與補缺分析：** 原文機制：先從各來源抽取 entities/relations，再跨來源 aggregate graphs，最後迭代 resolve duplicate entities 與 equivalent edges；官方方法段明訂勿把只是相似的概念錯併。補缺口判斷（本 repo 建議）：補 D03 的 entity resolution、relation normalization 與抽取資訊保留評估；屬 RAG 圖建構支援方法，其自建 MINE 是 benchmark，不能直接代替完整 RAG answer-quality 證據。 [原始來源：KGGen, Abstract／詳見閱讀範圍](https://proceedings.neurips.cc/paper_files/paper/2025/hash/2b368455e832d2b1a60bcad8c4c6481f-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D03；secondary_domains = D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀正式官方摘要、PDF封面及 §4 方法部分；其餘全文/實驗未完整核驗。

**版本注意：** 官方 proceedings landing page 只列7作者；PDF封面与arXivv2列9作者，含Joan Cabezas与Chris Cundy，此處採權威PDF封面9人。

**核對位置：** NeurIPS2025 official PDF p1 title/authors/Abstract, §4 pp3–4 method; official landing page DOI: https://proceedings.neurips.cc/paper_files/paper/2025/file/2b368455e832d2b1a60bcad8c4c6481f-Paper-Conference.pdf；arXiv2502.09956v2 authors/submission history。。

<a id="paper-meshrag"></a>
### MeshRAG

**完整標題：** [Collision to Cognition: Hash-Driven Graph Construction for Efficient RAG](https://aclanthology.org/2026.acl-long.1156/)。

**作者（本次核對版本）：** Chuang Zhou；Zheng Yuan；Linhao Luo；Zhaozhuo Xu；Yilin Xiao；Junnan Dong；Siyu An；di Yin；Xing Sun；Xiao Huang。

**書目：** 預印年份：未核得；正式出版年份：2026；已核 venue／狀態：ACL 2026。

**識別碼：** [DOI: 10.18653/v1/2026.acl-long.1156](https://doi.org/10.18653/v1/2026.acl-long.1156)。

**內容與補缺分析：** 以局部 hash collisions 誘導 chunk 關係與全局圖結構，研究減少顯式 triple extraction 的圖建構方式。 [原始來源：MeshRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2026.acl-long.1156/)。

**建議定位：** 方法論文；primary_domain = D04；secondary_domains = D05, D14。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** hash-based connections 不能僅憑摘要當成已驗證 semantic entailment；本次未核得關聯 arXiv ID。

**核對位置：** 官方 Abstract / publication metadata。

<a id="graph-control-memory"></a>
## 證據控制、圖式記憶與編排

| 候選與已核版本 | 補缺口軸 | 建議主／次領域 | 優先級 |
|---|---|---|---|
| [A2RAG](https://arxiv.org/abs/2601.21162) — arXiv 2026 | sufficiency 與 targeted refinement | D06／D05／D12 | P1 |
| [StructRAG](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html) — ICLR 2025 | task-conditioned context structuring | D07／D03／D05 | P1 |
| [Zep／Graphiti](https://arxiv.org/abs/2501.13956) — arXiv 2025 | bi-temporal graph memory | D11／D04／D05 | P1 |
| [DyG-RAG](https://arxiv.org/abs/2507.13396) — arXiv 2025 | event-centric temporal retrieval | D05／D03／D04／D09 | P2 |
| [KAG](https://arxiv.org/abs/2409.13731) — WWW Companion 2025 | 可執行 logical-form operators | D12／D04／D05 | P2 |
| [StructGPT](https://aclanthology.org/2023.emnlp-main.574/) — EMNLP 2023 | 結構化資料的讀取／推理介面 | D12／D05／D07 | P2 |
| [HybGRAG](https://aclanthology.org/2025.acl-long.43/) — ACL 2025 | textual＋relational retrieval 與 critic | D05／D12 | P2 |
| [GeAR](https://aclanthology.org/2025.findings-acl.624/) — Findings ACL 2025 | base retriever＋graph expansion | D05／D12 | P2 |
| [HydraRAG](https://aclanthology.org/2025.emnlp-main.730/) — EMNLP 2025 | cross-source verification | D05／D08／D12 | P2 |

P1 為上表第一批；P2 為後續按研究問題選讀。分類與優先級均待全文核對後定案。

<a id="paper-a2rag"></a>
### A2RAG

**完整標題：** [A2RAG: Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning](https://arxiv.org/abs/2601.21162)。

**作者（本次核對版本）：** Jiate Liu；Zebin Chen；Shaobo Qiao；Mingchen Ju；Danting Zhang；Bocheng Han；Shuyue Yu；Xin Shu；Jinglin Wu；Dong Wen；Xin Cao；Guanfeng Liu；Zhengyi Yang。

**書目：** 預印年份：2026；正式出版年份：未核得正式記錄；已核 venue／狀態：2026 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2601.21162](https://arxiv.org/abs/2601.21162)。

**內容與補缺分析：** 以 adaptive controller 驗證 evidence sufficiency，觸發 targeted refinement，並把 graph signals 回連來源文字。 [原始來源：A2RAG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2601.21162)。

**建議定位：** 方法論文；primary_domain = D06；secondary_domains = D05, D12。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** 已核 arXiv v2 摘要，2026-06-04；作者的 sufficiency 判定規則與實驗設定仍需全文核查。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-li2024-structrag"></a>
### StructRAG

**完整標題：** [StructRAG: Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html)。

**作者（本次核對版本）：** Zhuoqun Li；Xuanang Chen；Haiyang Yu；Hongyu Lin；Yaojie Lu；Qiaoyu Tang；Fei Huang；Xianpei Han；Le Sun；Yongbin Li。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：ICLR 2025。

**識別碼：** [arXiv:2410.08815](https://arxiv.org/abs/2410.08815)。

**內容與補缺分析：** 原文機制：task-conditioned router 選 table、graph、algorithm、catalogue 或 chunk；structurizer 從各文件抽取重組所需資訊，utilizer 分解問題並擷取結構中的相關知識。補缺口判斷（本 repo 建議）：補 D07 的 query-conditioned context structuring 與 D03/D05 接口，也可用來鬆開固定線性 pipeline；這不是全部任務均建立 graph 的方法。 [原始來源：StructRAG, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5975754c7650dfee0682e06e1fec0522-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D07；secondary_domains = D03, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀官方摘要、arXivv2 §3 方法與 §4 router 訓練段落；未完成正式全文版本比較及實驗核驗。

**核對位置：** ICLR2025 官方 Abstract/title/authors/venue；arXiv2410.08815v2 §3 Hybrid Structure Router, Scattered Knowledge Structurizer, Structured Knowledge Utilizer: https://arxiv.org/html/2410.08815v2#S3。。

<a id="paper-rasmussen2025-zep"></a>
### Zep／Graphiti

**完整標題：** [Zep: A Temporal Knowledge Graph Architecture for Agent Memory](https://arxiv.org/abs/2501.13956)。

**作者（本次核對版本）：** Preston Rasmussen；Pavlo Paliychuk；Travis Beauvais；Jack Ryan；Daniel Chalef。

**書目：** 預印年份：2025；正式出版年份：未核得正式記錄；已核 venue／狀態：2025 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2501.13956](https://arxiv.org/abs/2501.13956)。

**內容與補缺分析：** 原文機制：Graphiti 以 episode、semantic entity、community 三類 subgraph 保存對話記憶；bi-temporal timestamps 區分事實有效時間與系統攝入時間，新事實可使時間重疊且矛盾的舊 edge 失效，並以 cosine/BM25/BFS 取得記憶。補缺口判斷（本 repo 建議）：補 D11 圖式持續記憶、D04 異質節點層次與 D05 memory retrieval；Graphiti 是 Zep 此篇的核心元件，不能另算一篇，記憶更新也不直接等同 D10 外部來源同步。 [原始來源：Zep／Graphiti, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2501.13956)。

**建議定位：** 方法論文；primary_domain = D11；secondary_domains = D04, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀官方摘要及 arXivv1 §§2–3 方法段落；實驗與適用界線未完整核驗，非已驗證 primary note。

**版本注意：** 截至本次核對未由官方来源確認正式會議/期刊版本；不是宣告永無正式出版。

**核對位置：** arXiv2501.13956v1 Abstract; §2 Knowledge Graph Construction, §2.1 Episodes, §2.2.3 Temporal Extraction and Edge Invalidation, §3.1 Search: https://arxiv.org/html/2501.13956v1。。

<a id="paper-sun2025-dygrag"></a>
### DyG-RAG

**完整標題：** [DyG-RAG: Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning](https://arxiv.org/abs/2507.13396)。

**作者（本次核對版本）：** Qingyun Sun；Jiaqi Yuan；Shan He；Xiao Guan；Haonan Yuan；Xingcheng Fu；Jianxin Li；Philip S. Yu。

**書目：** 預印年份：2025；正式出版年份：未核得正式記錄；已核 venue／狀態：2025 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2507.13396](https://arxiv.org/abs/2507.13396)。

**內容與補缺分析：** 原文機制：Dynamic Event Units 將語義內容與時間錨點結合；DEUs 的 shared entities 與時間鄰近性建立 event graph，透過 time-aware traversal 取 event sequences，再使用 Time Chain-of-Thought 生成。補缺口判斷（本 repo 建議）：補 D03 event extraction / D04 event graph / D05 timeline retrieval；不能將時間鄰近性當已證實的因果關係，也不因 dynamic 名稱自動歸 D10 持續來源維護。 [原始來源：DyG-RAG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2507.13396)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D03, D04, D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 僅基於官方摘要整理，全文與所用因果/時間關係定義待查驗；正式出版未核實。

**核對位置：** arXiv2507.13396v1 Abstract/title/all8authors/submission history。。

<a id="paper-liang2024-kag"></a>
### KAG

**完整標題：** [KAG: Boosting LLMs in Professional Domains via Knowledge Augmented Generation](https://arxiv.org/abs/2409.13731)。

**作者（本次核對版本）：** Lei Liang；Mengshu Sun；Zhengke Gui；Zhongshu Zhu；Zhouyu Jiang；Ling Zhong；Yuan Qu；Peilong Zhao；Zhongpu Bo；Jin Yang；Huaidong Xiong；Lin Yuan；Jun Xu；Zaoyang Wang；Zhiqiang Zhang；Wen Zhang；Huajun Chen；Wenguang Chen；Jun Zhou。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：Companion Proceedings of the ACM on Web Conference 2025。

**識別碼：** [arXiv:2409.13731](https://arxiv.org/abs/2409.13731)；[DOI: 10.1145/3701716.3715240](https://doi.org/10.1145/3701716.3715240)。

**內容與補缺分析：** 原文機制（arXivv3）：圖與原文 chunks mutual-indexing；Logical Form Solver 以 retrieval、sort、math、deduce、output 等可執行函數規劃與解題，並在未解決時補充問題繼續迭代。補缺口判斷（本 repo 建議）：補 D12 的顯式執行計畫與 hybrid graph/text operators、D04 的 KG–chunk 互索引；其單次解題 global memory 不能直接當 D11 長期持續記憶。 [原始來源：KAG, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2409.13731)。

**建議定位：** 方法論文；primary_domain = D12；secondary_domains = D04, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已讀 arXiv 官方摘要及 v3 §§2.2–2.3 方法；正式出版 metadata 已核 ACM Crossref deposit，正式版全文與 preprint 差異待比較。

**關聯正式記錄作者：** Lei Liang；Zhongpu Bo；Zhengke Gui；Zhongshu Zhu；Ling Zhong；Peilong Zhao；Mengshu Sun；Zhiqiang Zhang；Jun Zhou；Wenguang Chen；Wen Zhang；Huajun Chen。此名單與上面的已讀 preprint 作者名單分開保存。

**版本注意：** arXivv3 19 作者；ACM正式 DOI deposit 12 作者，authors 欄保留所讀 preprint 的完整19人，published_authors另列正式12人。不得將兩版本內容直接宣告完全相同。

**核對位置：** arXiv2409.13731v3 §2.2 Mutual Indexing, §2.3 Logical Form Solver (Algorithms1–2 / Table1): https://arxiv.org/html/2409.13731v3#S2.SS3；formal ACM publisher-deposited DOI metadata: https://api.crossref.org/works/10.1145/3701716.3715240。。

<a id="paper-jiang2023-structgpt"></a>
### StructGPT

**完整標題：** [StructGPT: A General Framework for Large Language Model to Reason over Structured Data](https://aclanthology.org/2023.emnlp-main.574/)。

**作者（本次核對版本）：** Jinhao Jiang；Kun Zhou；Zican Dong；Keming Ye；Wayne Xin Zhao；Ji-Rong Wen。

**書目：** 預印年份：2023；正式出版年份：2023；已核 venue／狀態：EMNLP 2023。

**識別碼：** [arXiv:2305.09645](https://arxiv.org/abs/2305.09645)；[DOI: 10.18653/v1/2023.emnlp-main.574](https://doi.org/10.18653/v1/2023.emnlp-main.574)。

**內容與補缺分析：** 機制：Iterative Reading-then-Reasoning；以 specialised interfaces 取得 structured data evidence，再反覆 invoking–linearization–generation。補缺判斷：可補 KG/其他結構化資料的工具介面、證據線性化與 agent orchestration，避免 GraphRAG 只涵蓋從文本自建圖譜。Domain mapping 為本次分析建議；此文是跨 structured-data 方法，非 exclusively GraphRAG。 [原始來源：StructGPT, Abstract／詳見閱讀範圍](https://aclanthology.org/2023.emnlp-main.574/)。

**建議定位：** 方法論文；primary_domain = D12；secondary_domains = D05, D07。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；PDF 僅核 title page / Abstract；未核 structured interfaces 的全部種類或實驗全文。

**核對位置：** [metadata、Abstract、Submission history v1 (2023-05-16)](https://arxiv.org/abs/2305.09645)：預印年份與完整作者；[metadata、Abstract、citation DOI；pages 9237–9251](https://aclanthology.org/2023.emnlp-main.574/)：正式版本、EMNLP 2023、機制；Anthology 作者欄呈現 Xin Zhao；[PDF title page / Abstract](https://aclanthology.org/2023.emnlp-main.574.pdf)：正式 PDF 呈現 Wayne Xin Zhao。

<a id="paper-lee2024-hybgrag"></a>
### HybGRAG

**完整標題：** [HybGRAG: Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases](https://aclanthology.org/2025.acl-long.43/)。

**作者（本次核對版本）：** Meng-Chieh Lee；Qi Zhu；Costas Mavromatis；Zhen Han；Soji Adeshina；Vassilis N. Ioannidis；Huzefa Rangwala；Christos Faloutsos。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：ACL 2025。

**識別碼：** [arXiv:2412.16311](https://arxiv.org/abs/2412.16311)；[DOI: 10.18653/v1/2025.acl-long.43](https://doi.org/10.18653/v1/2025.acl-long.43)。

**內容與補缺分析：** 機制：對 semi-structured knowledge bases 的 textual+relational hybrid questions，使用 retriever bank 與 critic module，依 feedback 自動 refinement 並保留可解釋的 refinement path。補缺判斷：可補關係條件與文本條件共同決定答案的 retrieval routing / critique，與 graph/text 直接結果融合分開比較。Domain mapping 為本次分析建議。 [原始來源：HybGRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.acl-long.43/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D12。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；未核各 retriever、critic signal、refinement stopping rule 或實驗全文。

**核對位置：** [metadata、Abstract、Submission history v1 (2024-12-20)](https://arxiv.org/abs/2412.16311)：預印年份與作者；[metadata、Abstract、DOI；pp.879–893](https://aclanthology.org/2025.acl-long.43/)：正式 ACL 2025、retriever bank / critic mechanism。

<a id="paper-shen2024-gear"></a>
### GeAR

**完整標題：** [GeAR: Graph-enhanced Agent for Retrieval-augmented Generation](https://aclanthology.org/2025.findings-acl.624/)。

**作者（本次核對版本）：** Zhili Shen；Chenxin Diao；Pavlos Vougiouklis；Pascual Merita；Shriram Piramanayagam；Enting Chen；Damien Graux；Andre Melo；Ruofei Lai；Zeren Jiang；Zhongyang Li；Ye Qi；Yang Ren；Dandan Tu；Jeff Z. Pan。

**書目：** 預印年份：2024；正式出版年份：2025；已核 venue／狀態：Findings of ACL 2025。

**識別碼：** [arXiv:2412.18431](https://arxiv.org/abs/2412.18431)；[DOI: 10.18653/v1/2025.findings-acl.624](https://doi.org/10.18653/v1/2025.findings-acl.624)。

**內容與補缺分析：** 機制：以 graph expansion 增強 conventional base retriever（例如 BM25），再由 agent framework 將 graph-based retrieval 用於 multi-step retrieval。補缺判斷：可補保留既有 lexical/dense retriever 的 graph augmentation 路線，與完整替換 first-stage retriever 的 KG-only 方法分開比較。Domain mapping 為本次分析建議。 [原始來源：GeAR, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.findings-acl.624/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D12。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；authors 欄採正式 Anthology 15 位作者，不混入 v1 的 11 位作者順序；v1/current/正式版的方法與實驗差異待全文比對。

**核對位置：** [v1 metadata、Abstract、first submission (2024-12-24)](https://arxiv.org/abs/2412.18431v1)：預印年份；v1 列 11 位作者，與正式版不同；[current arXiv metadata](https://arxiv.org/abs/2412.18431)：目前 arXiv metadata 已列 15 位作者，與正式版本一致；名字大小寫呈現不同；[metadata、Abstract、DOI；pp.12049–12072](https://aclanthology.org/2025.findings-acl.624/)：正式 Findings ACL 2025、15 位作者、graph expansion / agent framework。

<a id="paper-tan2025-hydrarag"></a>
### HydraRAG

**完整標題：** [HydraRAG: Structured Cross-Source Enhanced Large Language Model Reasoning](https://aclanthology.org/2025.emnlp-main.730/)。

**作者（本次核對版本）：** Xingyu Tan；Xiaoyang Wang；Qing Liu；Xiwei Xu；Xin Yuan；Liming Zhu；Wenjie Zhang。

**書目：** 預印年份：未核得；正式出版年份：2025；已核 venue／狀態：EMNLP 2025。

**識別碼：** [DOI: 10.18653/v1/2025.emnlp-main.730](https://doi.org/10.18653/v1/2025.emnlp-main.730)。

**內容與補缺分析：** 機制：training-free 的 agent-driven graph/text exploration，結合 source trustworthiness、cross-source corroboration、entity-path alignment 三因素 cross-source verification 與 graph-based pruning。補缺判斷：可補 graph-centric retrieval 的多來源驗證與 D08 evidence reconciliation 介面；不因作者稱 verification 就推定其涵蓋所有權威性或充分性控制。Domain mapping 為本次分析建議。 [原始來源：HydraRAG, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.emnlp-main.730/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = D08, D12。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official_metadata_and_abstract_only；未核全文 reliability scoring、校準或實驗；未確認 arXiv / 初次預印年份，所以相關欄位為 null。

**核對位置：** [metadata、Abstract、DOI；pp.14431–14459](https://aclanthology.org/2025.emnlp-main.730/)：完整作者、正式 EMNLP 2025、cross-source verification mechanism。

<a id="graph-evaluation-security"></a>
## 評測、比較研究、Survey 與安全

| 候選與已核版本 | 補缺口軸 | 建議主／次領域 | 優先級 |
|---|---|---|---|
| [GraphRAG-Bench 論文](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html) — ICLR 2026 | 建圖→檢索→生成的任務評測 | D13／D04／D05／D09 | P1 |
| [WildGraphBench](https://aclanthology.org/2026.findings-acl.679/) — Findings ACL 2026 | 異質外部長文件評測 | D13／D05／D07／D09 | P1 |
| [Graph-CoT／GRBench](https://aclanthology.org/2024.findings-acl.11/) — Findings ACL 2024 | 圖推理方法與專用評測 | D05／D12／D13 | P2 |
| [PVLDB Unified Analysis](https://www.vldb.org/pvldb/vol18/p5623-zhou.pdf) — PVLDB 2025 | 共同設定與組件分析 | D13／D04／D05 | P1 |
| [Han et al. GraphRAG Survey](https://arxiv.org/abs/2501.00309) — arXiv 2024 | source／organizer 等分類視角 | CROSS（home；primary=null）／D04／D05／D07／D09 | P2 |
| [QO-Bench](https://arxiv.org/abs/2606.04646) — arXiv 2026（已接收） | query-operator preservation | D13／D03／D05／D09 | P2 |
| [GRADA](https://aclanthology.org/2025.emnlp-main.1132/) — EMNLP 2025 | document similarity graph 防禦 | D14／D05／D04 | P2 |
| [LogicPoison](https://aclanthology.org/2026.acl-long.252/) — ACL 2026 | graph-topology 攻擊 | D14／D04／D05 | P1 |

P1 為上表第一批；P2 為後續按研究問題選讀。分類與優先級均待全文核對後定案。

<a id="paper-xiang2025-graphragbench"></a>
### GraphRAG-Bench 論文

**完整標題：** [When to use Graphs in RAG: A Comprehensive Analysis for Graph Retrieval-Augmented Generation](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html)。

**作者（本次核對版本）：** Zhishang Xiang；Chuanjie Wu；Qinggang Zhang；Shengyuan Chen；Zijin Hong；Xiao Huang；Jinsong Su。

**書目：** 預印年份：2025；正式出版年份：2026；已核 venue／狀態：ICLR 2026。

**識別碼：** [arXiv:2506.05690](https://arxiv.org/abs/2506.05690)。

**內容與補缺分析：** 提出 GraphRAG-Bench，按事實查詢、複雜推理、脈絡摘要與創作任務，評估建圖、檢索與生成。值得補成獨立 evaluation anchor，讓圖結構收益的判斷帶有任務和比較條件；benchmark 和介紹它的論文只計一篇。 [原始來源：GraphRAG-Bench 論文, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html)。

**建議定位：** 評測論文；primary_domain = D13；secondary_domains = D04, D05, D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official proceedings abstract and bibliographic metadata only; full text not reviewed。

**核對位置：** ICLR 2026 official proceedings: abstract and author list；https://arxiv.org/abs/2506.05690: v1 2025-06-06; latest v3 2026-02-22。

<a id="paper-wang2026-wildgraphbench"></a>
### WildGraphBench

**完整標題：** [WildGraphBench: Benchmarking GraphRAG with Wild-Source Corpora](https://aclanthology.org/2026.findings-acl.679/)。

**作者（本次核對版本）：** Pengyu Wang；Benfeng Xu；Licheng Zhang；Shaohan Wang；Mingxuan Du；Chiwei Zhu；Zhendong Mao。

**書目：** 預印年份：2026；正式出版年份：2026；已核 venue／狀態：Findings of ACL 2026。

**識別碼：** [arXiv:2602.02053](https://arxiv.org/abs/2602.02053)；[DOI: 10.18653/v1/2026.findings-acl.679](https://doi.org/10.18653/v1/2026.findings-acl.679)。

**內容與補缺分析：** 用 Wikipedia 引用到的外部長文件作 corpus，並以帶引用的敘述建立事實、聚合與摘要問題。可補目前較缺的異質來源、長文件與細節保留評測，避免只用整理好的短段落評斷 GraphRAG。 [原始來源：WildGraphBench, Abstract／詳見閱讀範圍](https://aclanthology.org/2026.findings-acl.679/)。

**建議定位：** 評測論文；primary_domain = D13；secondary_domains = D05, D07, D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official abstract and bibliographic metadata only; full text not reviewed。

**核對位置：** ACL Anthology 2026.findings-acl.679: abstract, authors, venue, DOI and pp.13875–13890；https://arxiv.org/abs/2602.02053: v1 2026-02-02; v2 2026-02-03。

<a id="paper-jin2024-graphcot"></a>
### Graph-CoT／GRBench

**完整標題：** [Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs](https://aclanthology.org/2024.findings-acl.11/)。

**作者（本次核對版本）：** Bowen Jin；Chulin Xie；Jiawei Zhang；Kashob Kumar Roy；Yu Zhang；Zheng Li；Ruirui Li；Xianfeng Tang；Suhang Wang；Yu Meng；Jiawei Han。

**書目：** 預印年份：2024；正式出版年份：2024；已核 venue／狀態：Findings of ACL 2024。

**識別碼：** [arXiv:2404.07103](https://arxiv.org/abs/2404.07103)；[DOI: 10.18653/v1/2024.findings-acl.11](https://doi.org/10.18653/v1/2024.findings-acl.11)。

**內容與補缺分析：** 以 LLM reasoning、graph interaction 和 graph execution 交替進行圖上的推理，並介紹 GRBench。補 text-attributed graph 的 traversal 與評測；GRBench 在此論文內，和已收錄 G-Retriever 的 benchmark 分開，也不是 2026 同名 graph-relational database benchmark。 [原始來源：Graph-CoT／GRBench, Abstract／詳見閱讀範圍](https://aclanthology.org/2024.findings-acl.11/)。

**建議定位：** 方法論文＋GRBench 評測資源；primary_domain = D05；secondary_domains = D12, D13。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official abstract and bibliographic metadata only; full text not reviewed。

**核對位置：** ACL Anthology 2024.findings-acl.11: abstract, complete author list, venue, DOI and pp.163–184；https://arxiv.org/abs/2404.07103: v1 2024-04-10; latest v3 2024-10-03。

<a id="paper-zhou2025-graphragunifiedanalysis"></a>
### PVLDB Unified Analysis

**完整標題：** [In-Depth Analysis of Graph-Based RAG in a Unified Framework](https://www.vldb.org/pvldb/vol18/p5623-zhou.pdf)。

**作者（本次核對版本）：** Yingli Zhou；Yaodong Su；Youran Sun；Shu Wang；Taotao Wang；Runyuan He；Yongwei Zhang；Sicong Liang；Xilin Liu；Yuchi Ma；Yixiang Fang。

**書目：** 預印年份：2025；正式出版年份：2025；已核 venue／狀態：Proceedings of the VLDB Endowment 18(13)。

**識別碼：** [arXiv:2503.04338](https://arxiv.org/abs/2503.04338)；[DOI: 10.14778/3773731.3773738](https://doi.org/10.14778/3773731.3773738)。

**內容與補缺分析：** 以統一框架和共同實驗設定比較多種 graph-based RAG，涵蓋具体與抽象 QA。可補同條件比較及組件歸因，避免把不同 GraphRAG 系統的單篇結果直接排名；它是比較性實證研究，不能只因整理方法就當作 survey。 [原始來源：PVLDB Unified Analysis, Abstract／詳見閱讀範圍](https://www.vldb.org/pvldb/vol18/p5623-zhou.pdf)。

**建議定位：** 比較性實證研究（非 survey）；primary_domain = D13；secondary_domains = D04, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official abstract, first-page bibliographic block and publisher metadata only; full text and 2025/2026 version differences not reviewed。

**核對位置：** official PVLDB PDF first-page abstract and reference block: vol.18 no.13, pp.5623–5637, 2025, DOI；official publisher metadata https://doi.org/10.14778/3773731.3773738；https://arxiv.org/abs/2503.04338: v1 2025-03-06; latest v2 2026-04-27。

<a id="paper-han2024-graphragsurvey"></a>
### Han et al. GraphRAG Survey

**完整標題：** [Retrieval-Augmented Generation with Graphs (GraphRAG)](https://arxiv.org/abs/2501.00309)。

**作者（本次核對版本）：** Haoyu Han；Yu Wang；Harry Shomer；Kai Guo；Jiayuan Ding；Yongjia Lei；Mahantesh Halappanavar；Ryan A. Rossi；Subhabrata Mukherjee；Xianfeng Tang；Qi He；Zhigang Hua；Bo Long；Tong Zhao；Neil Shah；Amin Javari；Yinglong Xia；Jiliang Tang。

**書目：** 預印年份：2024；正式出版年份：未核得正式記錄；已核 venue／狀態：2024 預印；arXiv；正式出版未核。

**識別碼：** [arXiv:2501.00309](https://arxiv.org/abs/2501.00309)。

**內容與補缺分析：** 以 query processor、retriever、organizer、generator 和 data source 整理 GraphRAG，並強調不同 graph domains 的關係模式。可提供與 Peng 2408.08921 不同的 survey 視角，尤其釐清 graph source、retrieval 和 context organization；預印本首日是 2024-12-31，不能由 2501 ID 推為 2025。 [原始來源：Han et al. GraphRAG Survey, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2501.00309)。

**建議定位：** Survey；taxonomy_home = CROSS；primary_domain = null；secondary_domains = D04, D05, D07, D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official arXiv v2 abstract and metadata only; full text not reviewed; formal publication not verified。

**核對位置：** official arXiv abstract, authors and submission history: 2501.00309v1 2024-12-31; v2 2025-01-08。

<a id="paper-zhang2026-qobench"></a>
### QO-Bench

**完整標題：** [QO-Bench: Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples](https://arxiv.org/abs/2606.04646)。

**作者（本次核對版本）：** Mengao Zhang；Xiang Yang；Chang Liu；Tianhui Tan；Ke-wei Huang。

**書目：** 預印年份：2026；正式出版年份：未核得正式記錄；已核 venue／狀態：2026 預印；arXiv；註記已接收 Findings EMNLP 2026。

**識別碼：** [arXiv:2606.04646](https://arxiv.org/abs/2606.04646)。

**內容與補缺分析：** 以 typed event tuples 的確定性答案評估 filter、join、intersection、counting 等 query operators，並比較 RAG、ReAct RAG、GraphRAG 與 extraction-to-SQL。可補 D03 資訊保留到 D05 query execution 的 failure attribution；目前是官方 arXiv 註記已接收、正式 proceedings 尚未核對。 [原始來源：QO-Bench, Abstract／詳見閱讀範圍](https://arxiv.org/abs/2606.04646)。

**建議定位：** 評測論文；primary_domain = D13；secondary_domains = D03, D05, D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official arXiv v2 abstract and metadata only; full text and formal proceedings not reviewed。

**核對位置：** official arXiv v2 abstract, complete authors and comments: accepted to Findings of EMNLP 2026；submission history: v1 2026-06-03; v2 2026-09-08。

<a id="paper-zheng2025-grada"></a>
### GRADA

**完整標題：** [GRADA: Graph-based Reranking against Adversarial Documents Attack](https://aclanthology.org/2025.emnlp-main.1132/)。

**作者（本次核對版本）：** Jingjie Zheng；Aryo Pradipta Gema；Giwon Hong；Xuanli He；Pasquale Minervini；Youcheng Sun；Qiongkai Xu。

**書目：** 預印年份：2025；正式出版年份：2025；已核 venue／狀態：EMNLP 2025。

**識別碼：** [arXiv:2505.07546](https://arxiv.org/abs/2505.07546)；[DOI: 10.18653/v1/2025.emnlp-main.1132](https://doi.org/10.18653/v1/2025.emnlp-main.1132)。

**內容與補缺分析：** 利用 retrieved documents 之間的相似度圖與 score propagation，降低只對 query 高度相似的 adversarial documents 的影響。可補 D14 攻擊防禦与 D05 reranking 界面；此處的圖是 document similarity graph，不能直接當成 semantic knowledge graph 或 entity-relation extraction 方法。 [原始來源：GRADA, Abstract／詳見閱讀範圍](https://aclanthology.org/2025.emnlp-main.1132/)。

**建議定位：** 方法論文；primary_domain = D14；secondary_domains = D05, D04。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official abstract and metadata, plus §3.1–3.2 method excerpts; full paper and version differences not reviewed。

**核對位置：** ACL Anthology 2025.emnlp-main.1132: abstract, full authors, DOI and pp.22244–22266；official ACL PDF §3.1 Graph Construction and §3.2 Reranking, p.22247 (method excerpts)；https://arxiv.org/abs/2505.07546: submitted 2025-05-12; early title uses Reranker, formal title uses Reranking。

<a id="paper-xiao2026-logicpoison"></a>
### LogicPoison

**完整標題：** [LogicPoison: Logical Attacks on Graph Retrieval-Augmented Generation](https://aclanthology.org/2026.acl-long.252/)。

**作者（本次核對版本）：** Yilin Xiao；Jin Chen；Qinggang Zhang；Yujing Zhang；Chuang Zhou；Longhao Yang；Lingfei Ren；Xin Yang；Xiao Huang。

**書目：** 預印年份：2026；正式出版年份：2026；已核 venue／狀態：ACL 2026 (Long Papers)。

**識別碼：** [arXiv:2604.02954](https://arxiv.org/abs/2604.02954)；[DOI: 10.18653/v1/2026.acl-long.252](https://doi.org/10.18653/v1/2026.acl-long.252)。

**內容與補缺分析：** 研究 GraphRAG 的 topology integrity 失效，透過保持 entity type 的置換干擾全域連結和 query-specific reasoning bridges。值得作為 graph-specific security anchor，檢查看似合理的文字如何破壞多跳取證路徑；摘要所述效果不可推廣為所有 GraphRAG 防禦必然失效。 [原始來源：LogicPoison, Abstract／詳見閱讀範圍](https://aclanthology.org/2026.acl-long.252/)。

**建議定位：** 方法論文；primary_domain = D14；secondary_domains = D04, D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official abstract and bibliographic metadata only; full text and detailed threat model not reviewed。

**核對位置：** ACL Anthology 2026.acl-long.252: abstract, complete authors, venue, DOI and pp.5575–5591；https://arxiv.org/abs/2604.02954: v1 submitted 2026-04-03。

<a id="enabling-baselines"></a>
## 抽取支援與非圖式基線

| 候選與已核版本 | 補缺口軸 | 建議主／次領域 | 優先級 |
|---|---|---|---|
| [Re-DocRED](https://aclanthology.org/2022.emnlp-main.580/) — EMNLP 2022 | DocRED 漏標與 false negatives | D03／D13 | P2 |
| [GLiNER](https://aclanthology.org/2024.naacl-long.300/) — NAACL 2024 | 開放類型 entity recognition | D03 | P2 |
| [FiD](https://aclanthology.org/2021.eacl-main.74/) — EACL 2021 | 多篇 passages 的 reader 融合 | D07／D09 | P2 |
| [M3-Embedding／BGE-M3](https://aclanthology.org/2024.findings-acl.137/) — Findings ACL 2024 | dense／sparse／multi-vector | D04／D05 | P2 |
| [UPR](https://aclanthology.org/2022.emnlp-main.249/) — EMNLP 2022 | zero-shot passage reranking | D05 | P2 |
| [Nougat](https://proceedings.iclr.cc/paper_files/paper/2024/hash/a39a9aceda771cded859ae7560530e09-Abstract-Conference.html) — ICLR 2024 | scientific PDF 到 markup | D01 | P2 |

P1 為上表第一批；P2 為後續按研究問題選讀。分類與優先級均待全文核對後定案。

<a id="paper-tan2022-redocred"></a>
### Re-DocRED

**完整標題：** [Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction](https://aclanthology.org/2022.emnlp-main.580/)。

**作者（本次核對版本）：** Qingyu Tan；Lu Xu；Lidong Bing；Hwee Tou Ng；Sharifah Mahani Aljunied。

**書目：** 預印年份：2022；正式出版年份：2022；已核 venue／狀態：EMNLP 2022。

**識別碼：** [arXiv:2205.12696](https://arxiv.org/abs/2205.12696)；[DOI: 10.18653/v1/2022.emnlp-main.580](https://doi.org/10.18653/v1/2022.emnlp-main.580)。

**內容與補缺分析：** 分析 DocRED 的漏標與 false negatives，並重新標註形成 Re-DocRED。可補抽取 reliability 的評測資料基礎，區分模型漏抽和 gold annotation 漏標；Re-DocRED 是修訂資料集，不是新 GraphRAG method，也不能單靠 RE 評分證明 downstream RAG 改善。 [原始來源：Re-DocRED, Abstract／詳見閱讀範圍](https://aclanthology.org/2022.emnlp-main.580/)。

**建議定位：** 資料集／標註修訂論文；primary_domain = D03；secondary_domains = D13。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official published abstract and metadata only; full text and later arXiv revision differences not reviewed。

**核對位置：** ACL Anthology 2022.emnlp-main.580: abstract, full authors, venue, DOI and pp.8472–8487；https://arxiv.org/abs/2205.12696: v1 2022-05-25; v2 2022-10-25; later v3 2023-06-16。

<a id="paper-zaratiana2023-gliner"></a>
### GLiNER

**完整標題：** [GLiNER: Generalist Model for Named Entity Recognition using Bidirectional Transformer](https://aclanthology.org/2024.naacl-long.300/)。

**作者（本次核對版本）：** Urchade Zaratiana；Nadi Tomeh；Pierre Holat；Thierry Charnois。

**書目：** 預印年份：2023；正式出版年份：2024；已核 venue／狀態：NAACL 2024 (Long Papers)。

**識別碼：** [arXiv:2311.08526](https://arxiv.org/abs/2311.08526)；[DOI: 10.18653/v1/2024.naacl-long.300](https://doi.org/10.18653/v1/2024.naacl-long.300)。

**內容與補缺分析：** 以 bidirectional encoder 和文字化 entity types 做開放類型 NER。可補 graph construction 的 entity recognition 元件與受限資源的 extraction baseline；它不直接處理 relation extraction、entity linking 或 graph consolidation，並非端到端 GraphRAG 方法。 [原始來源：GLiNER, Abstract／詳見閱讀範圍](https://aclanthology.org/2024.naacl-long.300/)。

**建議定位：** 方法論文；primary_domain = D03；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** official published abstract and metadata only; full text not reviewed。

**核對位置：** ACL Anthology 2024.naacl-long.300: abstract, full authors, venue, DOI and pp.5364–5376；https://arxiv.org/abs/2311.08526: v1 submitted 2023-11-14。

<a id="paper-fid"></a>
### FiD

**完整標題：** [Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering](https://aclanthology.org/2021.eacl-main.74/)。

**作者（本次核對版本）：** Gautier Izacard；Edouard Grave。

**書目：** 預印年份：2020；正式出版年份：2021；已核 venue／狀態：EACL 2021。

**識別碼：** [arXiv:2007.01282](https://arxiv.org/abs/2007.01282)；[DOI: 10.18653/v1/2021.eacl-main.74](https://doi.org/10.18653/v1/2021.eacl-main.74)。

**內容與補缺分析：** 研究 generative reader 如何聚合多篇檢索 passages 的證據。 [原始來源：FiD, Abstract／詳見閱讀範圍](https://aclanthology.org/2021.eacl-main.74/)。

**建議定位：** 方法論文；primary_domain = D07；secondary_domains = D09。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-m3-embedding"></a>
### M3-Embedding／BGE-M3

**完整標題：** [M3-Embedding: Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation](https://aclanthology.org/2024.findings-acl.137/)。

**作者（本次核對版本）：** Jianlyu Chen；Shitao Xiao；Peitian Zhang；Kun Luo；Defu Lian；Zheng Liu。

**書目：** 預印年份：2024；正式出版年份：2024；已核 venue／狀態：Findings of ACL 2024。

**識別碼：** [arXiv:2402.03216](https://arxiv.org/abs/2402.03216)；[DOI: 10.18653/v1/2024.findings-acl.137](https://doi.org/10.18653/v1/2024.findings-acl.137)。

**內容與補缺分析：** 單一 embedding 模型支援 dense、sparse、multi-vector retrieval 與不同文本粒度。 [原始來源：M3-Embedding／BGE-M3, Abstract／詳見閱讀範圍](https://aclanthology.org/2024.findings-acl.137/)。

**建議定位：** 方法論文；primary_domain = D04；secondary_domains = D05。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**版本注意：** 正式版本使用 M3-Embedding 與作者 Jianlyu Chen；arXiv 標題加 BGE，作者拼作 Jianlv Chen，未逐章比較版本。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-upr"></a>
### UPR

**完整標題：** [Improving Passage Retrieval with Zero-Shot Question Generation](https://aclanthology.org/2022.emnlp-main.249/)。

**作者（本次核對版本）：** Devendra Sachan；Mike Lewis；Mandar Joshi；Armen Aghajanyan；Wen-tau Yih；Joelle Pineau；Luke Zettlemoyer。

**書目：** 預印年份：2022；正式出版年份：2022；已核 venue／狀態：EMNLP 2022。

**識別碼：** [arXiv:2204.07496](https://arxiv.org/abs/2204.07496)；[DOI: 10.18653/v1/2022.emnlp-main.249](https://doi.org/10.18653/v1/2022.emnlp-main.249)。

**內容與補缺分析：** 以 passage 條件下產生原 query 的機率重新排序候選段落，使用 zero-shot question generation。 [原始來源：UPR, Abstract／詳見閱讀範圍](https://aclanthology.org/2022.emnlp-main.249/)。

**建議定位：** 方法論文；primary_domain = D05；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="paper-nougat"></a>
### Nougat

**完整標題：** [Nougat: Neural Optical Understanding for Academic Documents](https://proceedings.iclr.cc/paper_files/paper/2024/hash/a39a9aceda771cded859ae7560530e09-Abstract-Conference.html)。

**作者（本次核對版本）：** Lukas Blecher；Guillem Cucurull；Thomas Scialom；Robert Stojnic。

**書目：** 預印年份：2023；正式出版年份：2024；已核 venue／狀態：ICLR 2024。

**識別碼：** [arXiv:2308.13418](https://arxiv.org/abs/2308.13418)。

**內容與補缺分析：** 以視覺模型將 scientific document 頁面轉為 markup，涵蓋數學表達式等結構。 [原始來源：Nougat, Abstract／詳見閱讀範圍](https://proceedings.iclr.cc/paper_files/paper/2024/hash/a39a9aceda771cded859ae7560530e09-Abstract-Conference.html)。

**建議定位：** 方法論文；primary_domain = D01；secondary_domains = []。這是本 repo 的候選 mapping，非作者提出的 taxonomy。

**閱讀範圍：** 已核官方 metadata 與摘要；全文待驗證。

**核對位置：** 官方 Abstract / publication metadata。

<a id="taxonomy-version-boundaries"></a>
## 分類與版本邊界

- **Graph 的物件與角色分開記錄。** G-RAG 涉及跨文件／AMR，GRADA 是 document similarity graph，GRAG 是 textual subgraph，KGQA 方法則處理已有 KG；不能因 graph 字樣就都當作從原文抽取的 semantic KG。各項來源見上方 G-RAG、GRADA、GRAG、ToG 條目。
- **HyperRAG 同名但不同研究。** Lien et al. WWW 2026 處理 n-ary hypergraphs（arXiv:2602.14470）；Zhou et al. ACL 2026 的 HyperRAG 使用 hyperbolic space（2026.acl-long.986）。HyperGraphRAG（2503.21322）是另一篇。各自已有獨立官方識別碼，不能查重合併。
- **CatRAG 同名需識別碼辨認。** 本頁只列 Traversal（2602.01965／2026.findings-acl.290），不混入 CatRAG Debiasing（2603.21524）。[Traversal 正式記錄](https://aclanthology.org/2026.findings-acl.290/)；[Debiasing 預印本](https://arxiv.org/abs/2603.21524)。
- **D06 不等於 D05 證據鏈 Recall。** A2RAG 摘要明述 sufficiency controller／targeted refinement，故暫列 D06；CatRAG 提升 query-aware traversal 與 reasoning completeness，暫列 D05，不能由摘要推導完整 sufficiency 判定。來源見上述兩條。
- **Dynamic／Memory 名稱不直接決定分類。** DynaGRAG 的 query BFS 不證明 D10 update lifecycle；DyG-RAG 的 time-aware event retrieval 不證明 source synchronization；HyperRAG 的 parametric HyperMemory 不直接屬 D11。Zep 的 Graphiti 是同篇記憶架構元件，並非第二篇。來源見各條。
- **Survey、比較研究、benchmark、dataset 保持分流。** Han survey 是 CROSS 候選；PVLDB 文獻是比較性實證研究；GraphRAG-Bench 是介紹 benchmark 的一篇論文；Graph-CoT／GRBench 只計一篇；Re-DocRED 是不同 ID 的修訂資料集，不能和 DocRED 當同一項，也不是 GraphRAG method。來源見各條。
- **正式與預印版本需繼續比對。** PathRAG 是 2025 預印／AAAI 2026 正式版；Han survey 的 2501 ID 首次提交為 2024-12-31；QO-Bench 有已接收註記但正式 proceedings 未核。KAG 的已讀 preprint 19 作者與正式 metadata 12 作者分開列；KGGen 依官方 PDF 封面九作者，不沿用 landing page 七人名單。來源與已讀範圍見各條。

<a id="checks-and-limits"></a>
## 查核方式與限制

本次由三個並行子任務查 graph retrieval、graph construction／memory、evaluation／security；主 agent 另查 GNN-RAG、GRAG、OG-RAG、KG-FiD、A2RAG、CatRAG、MeshRAG 與非圖基線，彙整後再依 arXiv、DOI、正規化完整標題查重。44 項識別碼／標題均未與既有 177 篇 paper records 重複；Notes／Papers 檔名沒有相符工件。

已完成：官方 title／authors／年份／已找到的 venue 與識別碼核對；預印與正式出版區分；候選間同名與版本辨識；各項閱讀範圍標示；D01–D14／CROSS 建議合法性檢查。未知 DOI／預印年份／正式版本留未核，未以 ID 前綴推算年份。

限制：這不是系統性 review，也不是截至該日所有 GraphRAG 論文的全集。未全面讀取 129 個既有 PDF 的 references；「未見提及」限 repo Markdown 及檔名。多數候選只讀摘要；有些官方 publisher landing page 受阻，以 publisher-deposited Crossref metadata 核書目並保留 arXiv 機制來源。沒有重新驗證各方法的實驗表格、性能、API 成本、硬體條件或所有版本差異。

後續建立 paper notes 時，依 [[AGENTS|AGENTS.md]] 補齊七個標準板塊，並優先核：任務／資料集、模型／context budget、硬體／API 成本、記憶體／延遲／吞吐量、retrieval／generation 品質、失效情境／維護複雜度。缺少條件保持待驗證；跨實驗環境的分數標「不可直接比較」。本次不由摘要寫出性能排名。

候選尚未納入成熟 survey coverage；完成全文核對後，真正的 survey-level Domain coverage 仍只在 [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]] 維護。
