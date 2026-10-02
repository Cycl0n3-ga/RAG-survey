---
title: "GraphRAG Supplementation Review — 2026-10-02"
tags: [literature-audit, graph-rag, version-verification]
last_updated: "2026-10-03"
audit_scope: "44 supplemented papers; identifier checks against 221 paper records"
review_mode: "single-agent; structural audit plus targeted full-text checks"
taxonomy_version: "v2"
---

# GraphRAG 補齊成果複核

44 篇新增候選均已有標準筆記與可讀本地 PDF，但先前的進度頁、分類與部分證據敘述需要修正。本次完成格式／檔案／識別碼檢查，並抽查四篇的原文內容；不宣稱重新逐篇核完 44 篇全部實驗，也不把「收錄完成」解讀為「正式版本比對完成」。補齊清單見 [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Literature Coverage Gaps - 2026-10-02|44 篇補齊進度]]。

**2026-10-03 後續更新：** 已核 CatRAG、M3 官方 PDF 的指定文字／表格，修正 M3 分數、頁碼／作者拼寫界線並補正式版資訊；KAG 再核書目及本地表格，正式全文仍待取得。下方 manifest 同步最新狀態；原 2026-10-02 的檢查結果與修正記錄保留。詳細差異見 [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Version Verification - 2026-10-03|三篇版本核對報告]]。

## 已修正的問題

| 問題 | 修正與證據界線 |
|---|---|
| GNN-RAG 的訓練時間／記憶體混寫 | 原筆記把下游 LLM 的訓練條件與 GNN 的 memory 數字拼在一起。Appendix D.3（p. 16698；PDF p. 17）實際分別報：2 張 A100-80G 的下游 LLM，30K 資料／1 epoch 超過 12 小時；RTX 3090 的 GNN，相同資料量／epoch 少於 15 分鐘且少於 8GB。已拆開並標示不同模型／硬體。 |
| KGGen 的成本表與指標解讀 | KGGen 成本在 Table 3；GraphRAG 時間在 Table 4。已改為 Tables 3–4（p. 10），保留原文 2,079.17／2,319 秒不一致，成因未核。Table 1(b) 的 98／0／55% 是作者定義的 KG 三元組結構合規率，不是事實正確率（§6.4，p. 8）。 |
| CatRAG 的預印題名錯誤 | arXiv v1 的題名是 *Breaking the Static Graph: Context-Aware Traversal for Robust Retrieval-Augmented Generation*；正式題名末段是 *for Graph-Based RAG*。已修正文、PDF 檔名與所有該路徑引用，保留正式版作筆記 canonical title。 |
| Graph 方法的 lifecycle 分類混用 | ReGraphRAG 保留 D05 主域／D07 次域；CatRAG 保留 D05／D13。兩者 query-time 重組或權重調整不另當作 D04 corpus-side indexing 貢獻。HyperGraphRAG 候選細項誤植為 D05，已同步標準筆記的 D04／D03／D05；候選頁 44 個 mapping 與筆記對齊。 |
| ReGraphRAG 的鏡像驗證宣稱過廣 | LFS SHA-256 相符只支持鏡像檔案完整；不能證明與 ACL 官方 binary 相同。已限定為首頁、頁碼、已核方法／Tables 1–4 相符，附錄 A／F 圖像已核；官方 binary identity 尚未比對。 |
| 三篇 `year: null` | ReGraphRAG、hyperbolic HyperRAG、MeshRAG 改用最早可核正式發表年 2025／2026／2026，並加 `year_basis: earliest_verified_publication`。未核更早預印，`arxiv: null` 保留，不聲稱不存在其他版本。 |
| 索引與連結不同步 | 移除 ReGraphRAG 過時的 PDF pending；修正索引表格內未跳脫的 wikilink 分隔符、GeAR 三條缺少分類目錄的連結，以及候選頁仍寫摘要／全文待核的舊狀態。D04／D05 primary 筆記數更新為 12／41。 |
| 全文版本缺少可查詢欄位 | 44 篇新增 `source_version`、`verified_version`、`pdf_pages`、`pdf_sha256`；CatRAG 另加 `source_title`。FiD 明定本地為 arXiv v2；另有正式全文證據的三篇以 `additional_verified_versions` 記錄範圍。原有 metadata 保留。 |

GNN-RAG 的資源條件依 [ACL 正式全文 Appendix D.3](https://aclanthology.org/2025.findings-acl.856.pdf) 視覺核對；KGGen 的表格／指標依 [NeurIPS 正式全文 Tables 1、3–4、§6.4](https://proceedings.neurips.cc/paper_files/paper/2025/file/2b368455e832d2b1a60bcad8c4c6481f-Paper-Conference.pdf) 核對。CatRAG 的兩個題名分別由 [arXiv v1](https://arxiv.org/abs/2602.01965v1) 與 [ACL 正式紀錄](https://aclanthology.org/2026.findings-acl.290/) 支持。ReGraphRAG 的正式書目依 [ACL entry](https://aclanthology.org/2025.findings-emnlp.290/)，鏡像完整性依 [固定資料集 commit](https://huggingface.co/datasets/Chelsea707/Conference_2020-2025/commit/0be08ad5751d514d28cc9477c4b9acbcad3a646c)。分類是依 repo [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|lifecycle boundaries]] 所做的判斷，不是作者的分類結論。

## 檢查範圍與結果

- 44/44 筆記具備規定 metadata 與實際七個核心 H2 板塊；`year` 為整數，`publication_year` 為整數或 null，list 欄位型別與封閉 paradigm 字典合法。
- 44/44 本地 PDF 非空、可解析；檔案頁數／完整 SHA-256 與 metadata 相符。29 份 arXiv 檔的論文本身版本 stamp 均與 `source_version` 相符；正式格式檔依題名與會議標頭辨識。這不是出版社 binary 的共同 hash 查驗。
- 44 篇的 `paper_id`、非空 DOI／arXiv ID 未與全庫 221 篇 paper records 重複。這是識別碼查重，不宣稱所有擴充版本的內容完全相同。
- 共檢查 669 條本地連結；新增筆記、進度與文獻索引中的本地 PDF／筆記連結可解析；候選細項 taxonomy 與標準筆記一致。CatRAG PDF 只改名，檔案內容與 hash 未改。
- 內容抽查包括 ReGraphRAG Tables 1–2 的平均勝率／消融、CatRAG §3 與 Limitations、GNN-RAG Appendix D.3、KGGen Tables 3–4／§6.4。沒有跨論文分數排名。Markdown fence／Mermaid subgraph 配對與 `git diff --check` 通過。

`source_version` 表示實際保存的本地全文版本；`verified_version` 表示筆記所列證據已核的本地版本，不是所有歷史版的完整核驗宣告。GeAR、HybGRAG、StructGPT，以及 2026-10-03 補核的 CatRAG、M3 另核過正式全文指定證據，範圍以 `additional_verified_versions` 與正文記錄；欄位不替代詳細閱讀範圍。`pdf_sha256` 用於辨認檔案是否改變，不能單獨證明內容正確。

## 44 篇本地版本清單

本地來源共 29 份 arXiv 全文、15 份 proceedings-format／published PDFs（含 ReGraphRAG 第三方鏡像）。下表的正式版追蹤狀態依筆記已明示範圍整理；「差異待比對」不表示本地全文尚未閱讀。

| 筆記 ID | 主域／home | 本地全文版本 | PDF 頁數 | 正式版追蹤狀態 |
|---|---|---|---:|---|
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph\|Sun2024_ThinkOnGraph]] | D05 | ICLR 2024 proceedings | 31 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning\|Luo2024_ReasoningOnGraphs]] | D05 | ICLR 2024 proceedings | 24 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation\|Li2025_SubgraphRAG]] | D05 | ICLR 2025 proceedings | 29 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs\|Mavromatis2025_GNNRAG]] | D05 | Findings ACL 2025 proceedings | 18 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(AAAI 2026-03) PathRAG - Pruning Graph-Based Retrieval Augmented Generation with Relational Paths\|Chen2026_PathRAG]] | D05 | AAAI 2026 proceedings | 9 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) HyperGraphRAG - Retrieval-Augmented Generation via Hypergraph-Structured Knowledge Representation\|Luo2025_HyperGraphRAG]] | D04 | NeurIPS 2025 proceedings | 29 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) OG-RAG - Ontology-grounded Retrieval-Augmented Generation for Large Language Models\|Sharma2025_OG-RAG]] | D04 | EMNLP 2025 proceedings | 20 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) KGGen - Extracting Knowledge Graphs from Plain Text with Language Models\|Mo2025_KGGen]] | D03 | NeurIPS 2025 proceedings | 24 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) StructRAG - Boosting Knowledge Intensive Reasoning of LLMs via Inference-time Hybrid Information Structurization\|Li2025_StructRAG]] | D07 | ICLR 2025 proceedings | 18 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2026-01) A2RAG - Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning\|Liu2026_A2RAG]] | D06 | arXiv:2601.21162v2 | 10 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2025-01) Zep - A Temporal Knowledge Graph Architecture for Agent Memory\|Rasmussen2025_Zep]] | D11 | arXiv:2501.13956v1 | 12 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2026-07) Breaking the Static Graph - Context-Aware Traversal for Graph-Based RAG\|Lau2026_CatRAGTraversal]] | D05 | arXiv:2602.01965v1 | 13 | 正式全文指定文字／表格已比對；圖像等差異未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2026-04) When to Use Graphs in RAG - A Comprehensive Analysis for Graph Retrieval-Augmented Generation\|Xiang2026_WhenToUseGraphsInRAG]] | D13 | ICLR 2026 proceedings | 34 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2026-07) WildGraphBench - Benchmarking GraphRAG with Wild-Source Corpora\|Wang2026_WildGraphBench]] | D13 | arXiv:2602.02053v2 | 18 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(PVLDB 2025-09) In-depth Analysis of Graph-based RAG in a Unified Framework\|Zhou2025_UnifiedGraphRAGAnalysis]] | D13 | PVLDB 2025 published article | 15 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2026-07) LogicPoison - Logical Attacks on Graph Retrieval-Augmented Generation\|Xiao2026_LogicPoison]] | D14 | arXiv:2604.02954v1 | 16 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation\|Ma2024_ToG2]] | D05 | ICLR 2025 proceedings | 25 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation\|Hu2024_GRAG]] | D05 | arXiv:2405.16506v3 | 13 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2022-05) KG-FiD - Infusing Knowledge Graph in Fusion-in-Decoder for Open-Domain Question Answering\|Yu2021_KGFID]] | D05 | arXiv:2110.04330v2 | 14 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) SimGRAG - Leveraging Similar Subgraphs for Knowledge Graphs Driven Retrieval-Augmented Generation\|Cai2024_SimGRAG]] | D05 | arXiv:2412.15272v2 | 20 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-05) Don’t Forget to Connect! Improving RAG with Graph-based Reranking\|Dong2024_GRAGReranking]] | D05 | arXiv:2405.18414v1 | 19 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2025-01) Fast Think-on-Graph - Wider, Deeper and Faster Reasoning of Large Language Model on Knowledge Graph\|Liang2025_FastToG]] | D05 | arXiv:2501.14300v1 | 11 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW 2025-04) Paths-over-Graph - Knowledge Graph Empowered Large Language Model Reasoning\|Tan2024_PoG]] | D05 | arXiv:2410.14211v4 | 18 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-12) DynaGRAG - Exploring the Topology of Information for Advancing Language Understanding and Generation in Graph Retrieval-Augmented Generation\|Thakrar2024_DynaGRAG]] | D05 | arXiv:2412.18644v3 | 17 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW 2026-04) HyperRAG - Reasoning N-ary Facts over Hypergraphs for Retrieval Augmented Generation\|Lien2026_HyperRAG_Nary]] | D05 | arXiv:2602.14470v1 | 12 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2026-07) Query-Aware Knowledge Retrieval via Hyperbolic Structuring\|Zhou2026_HyperRAG_Hyperbolic]] | D04 | ACL 2026 proceedings-format PDF | 14 | 本地為正式格式；歷史版本未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2026-07) Collision to Cognition - Hash-Driven Graph Construction for Efficient RAG\|Zhou2026_MeshRAG]] | D04 | ACL 2026 proceedings-format author copy | 17 | 作者提供正式格式檔；未做官方 binary 比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings EMNLP 2025-11) ReGraphRAG - Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation\|Kim2025_ReGraphRAG]] | D05 | Findings EMNLP 2025 proceedings-format third-party mirror | 18 | 鏡像證據已核；ACL binary 未比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2025-07) DyG-RAG - Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning\|Sun2025_DyGRAG]] | D05 | arXiv:2507.13396v1 | 18 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation\|Liang2025_KAG]] | D12 | arXiv:2409.13731v3 | 33 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2023-12) StructGPT - A General Framework for Large Language Model to Reason over Structured Data\|Jiang2023_StructGPT]] | D12 | arXiv:2305.09645v2 | 15 | 正式全文指定證據亦已核；完整差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases\|Lee2025_HybGRAG]] | D05 | arXiv:2412.16311v2 | 15 | 正式全文指定證據亦已核；完整差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation\|Shen2024_GeAR]] | D05 | arXiv:2412.18431v2 | 24 | 正式全文指定證據亦已核；完整差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) GRADA - Graph-based Reranking against Adversarial Documents Attack\|Zheng2025_GRADA]] | D14 | arXiv:2505.07546v3 | 23 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2025-01) Retrieval-Augmented Generation with Graphs (GraphRAG)\|Han2024_GraphRAGSurvey]] | CROSS | arXiv:2501.00309v2 | 88 | 正式出版紀錄未核得 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2026-06) QO-Bench - Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples\|Zhang2026_QOBench]] | D13 | arXiv:2606.04646v2 | 19 | accepted；正式 proceedings 待核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) Graph Chain-of-Thought - Augmenting Large Language Models by Reasoning on Graphs\|Jin2024_GraphCoT_GRBench]] | D05 | arXiv:2404.07103v3 | 22 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Revisiting DocRED - Addressing the False Negative Problem in Relation Extraction\|Tan2022_ReDocRED]] | D03 | arXiv:2205.12696v3 | 16 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EACL 2021-04) Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering\|Izacard2021_FusionInDecoder]] | D07 | arXiv:2007.01282v2 | 6 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NAACL 2024-06) GLiNER - Generalist Model for Named Entity Recognition using Bidirectional Transformer\|Zaratiana2023_GLiNER]] | D03 | arXiv:2311.08526v1 | 11 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) M3-Embedding - Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation\|Chen2024_M3Embedding]] | D04 | arXiv:2402.03216v5 | 18 | 正式全文指定文字／表格已比對；圖像等差異未全核 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2022-12) Improving Passage Retrieval with Zero-Shot Question Generation\|Sachan2022_UPR]] | D05 | arXiv:2204.07496v4 | 18 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Nougat - Neural Optical Understanding for Academic Documents\|Blecher2023_Nougat]] | D01 | arXiv:2308.13418v1 | 17 | 正式版全文／版本差異待比對 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) HydraRAG - Structured Cross-Source Enhanced Large Language Model Reasoning\|Tan2025_HydraRAG]] | D05 | arXiv:2505.17464v4 | 29 | 正式版全文／版本差異待比對 |

## 還需要改善的工作

**正式版差異核對優先於繼續累積 GraphRAG 數量。** 29 份本地 arXiv 來源中，21 篇已有正式出版 metadata。截至 2026-10-03，共 5 篇另核正式全文指定證據（GeAR、HybGRAG、StructGPT、CatRAG、M3），完整文字／公式／圖像差異仍未全部核完。CatRAG 的新增基線／效率／案例與 M3 的主要表格／資源已比對；優先繼續取得 KAG 正式 10 頁全文，再核其他已有出版 metadata 的版本。這是 repo 的查核順序建議，不代表未讀版本必然有實質改變。

ReGraphRAG 可在 ACL 下載可用時保存官方檔並比較 checksum／內容。QO-Bench 的接收註記應在正式 proceedings 發布後核 venue、DOI、作者與數字；本地目前仍是 arXiv v2。KGGen 的時間差異需要作者說明或可重現實作佐證，現階段保留原文矛盾。

**比較資訊還需按同條件整理。** 部分筆記仍缺硬體、API 費用或 context budget，原文沒有提供時不填推算值。下一輪可按 KGQA、多文件 QA、全局摘要與記憶分組，固定資料集／reader／token budget，再並列檢索、生成、成本與失效模式；不同條件維持「不可直接比較」。本輪新增來源的機制差異不構成整體系統性能排名。

**後續覆蓋應回到 D01–D14 缺口。** 本庫 primary counts 為 D05=41、D04=12、D02=5、D06=7、D10=1；數量不代表成熟度或研究價值，但可見本輪圖檢索比知識維護等問題更集中。後續補文獻以 parsing error propagation、segmentation 評測、sufficiency calibration 與 index/source maintenance 等具體問題為目標，勿僅按 X-RAG 名稱擴張。這是未來搜尋方向，尚未當作 survey-backed findings 登錄。

**既有 anchor 也有個別維護缺口。** [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2025-12) GFM-RAG - Graph Foundation Model for Retrieval Augmented Generation|GFM-RAG]] 不屬這 44 篇新增候選；其 `pdf_file` 仍為 null，正文只有摘要／taxonomy／source，缺七板塊與全文證據範圍。應列入後續維護，不能由它已有筆記或 `verified` 值就推定本地全文與實驗整理齊全。本次 44/44 結論只適用新增清單。

Domain-level survey coverage 仍只由 [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]] 維護；Han survey 已列入該索引，44 篇方法／benchmark／dataset 筆記不會自動變成各 Domain 的成熟 survey 證據。
