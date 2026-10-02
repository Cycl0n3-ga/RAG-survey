---
paper_id: "Kim2025_ReGraphRAG"
title: "ReGraphRAG: Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation"
authors:
  - "Soohyeong Kim"
  - "Seok Jun Hwang"
  - "JungHyoun Kim"
  - "Jeonghyeon Park"
  - "Yong Suk Choi"
year: null
publication_year: 2025
venue: "Findings of the Association for Computational Linguistics: EMNLP 2025"
doi: "10.18653/v1/2025.findings-emnlp.290"
arxiv: null
url: "https://aclanthology.org/2025.findings-emnlp.290/"
pdf_file: null
tags:
  - paper
  - fragmented-knowledge-graphs
  - graph-reorganization
verification_status: "pending_verification"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D04"
primary_domain: "D04"
secondary_domains:
  - "D03"
  - "D05"
paradigm_tags:
  - "graph_rag"
adjacent_interfaces: []
research_questions:
  - "graph_reorganization"
  - "multi_perspective_retrieval"
  - "query_aware_reranking"
benchmark_ids: []
dataset_ids:
  - "Ultradomain"
metrics:
  - "Comprehensiveness pairwise win rate"
  - "Diversity pairwise win rate"
  - "Empowerment pairwise win rate"
  - "Overall pairwise win rate"
---

# ReGraphRAG: Reorganizing Fragmented Knowledge Graphs for Multi-Perspective Retrieval-Augmented Generation

> **全文待取得／核驗：** 書目資訊由 ACL Anthology entry 與 DOI 核對。ACL 官方 PDF 搜尋索引目前可讀到引言、方法、實驗設定、Table 1 摘錄與限制段落；以下只記錄這些可定位內容。PDF 本體在本環境下載逾時，故尚未逐頁閱讀、核驗完整表格與附錄，也沒有本地 PDF。`verification_status` 保持 `pending_verification`，不可視為全文已讀完。

## 一話摘要 (TL;DR)
ReGraphRAG 在查詢時把檢索到的碎裂子圖重組為連通子圖，並以多視角子查詢擴展證據，再按原查詢重排三元組；官方 PDF 索引中 LightRAG 對照區塊的 Ultradomain 平均 Diversity win rate 顯示 ReGraphRAG 為 92.4%（Table 1，仍需全文核驗表格完整設定）。

## 研究背景與問題定義 (Problem Statement)
論文指出，從非結構化文件抽出的圖可能含許多互不相連的節點與子圖；因此即使圖中存在相關事實，檢索到的片段仍可能不足以串接多跳推理。引言將 LightRAG 作為可視化比較例，指出其檢索到的子圖可能仍是分散片段（Figure 1，pp. 5426–5427）。碎裂程度的量化與更多背景證據待全文核驗。[官方 PDF 索引，Introduction／Figure 1]

## 核心方法與技術架構 (Methodology & Architecture)
方法索引摘錄描述三個順序相連的模組：

1. **Graph Reorganization**：在互不相連的檢索子圖之間尋找有意義的最短路徑，加入連接邊，把片段組成連通子圖。
2. **Perspective Expansion**：把原查詢分解成多個詮釋角度，為各角度生成子查詢並檢索補充子圖；若三元組出現在多個視角，prompt 將其去重後置於共同視角，減少冗餘。
3. **Query-aware Reranking**：把結果整理為 `(node_i, edge_ij, node_j)` 三元組，以邊／三元組 embedding 與原查詢表示的 cosine similarity 排序，再供生成器使用。論文索引摘錄亦呈現以 `[Perspective]` 格式明示節點關係所屬視角的 prompt。

實際路徑搜尋、連接邊產生方式、embedding 模型與各模組參數仍待 PDF 全文及附錄核驗。[官方 PDF 索引，§3、§4.4，pp. 5428–5431]

## 主要實驗結果與證據 (Empirical Results & Evidence)
官方實驗索引稱採 LightRAG 的評估協議，使用 Ultradomain（由 18 個領域大學教科書構成），取 Agriculture、Computer Science、Legal 三個領域及混合領域 Mix。基線為 NaïveRAG、HyDE、GraphRAG、LightRAG；其中作者明確指出 LightRAG 與 ReGraphRAG 共用同一份從原文件建出的知識圖譜。LLM 對系統回答作成對比較，評估 Comprehensiveness、Diversity、Empowerment、Overall 四個面向，win rate 是回答被偏好的比例。官方索引中的 Table 1 摘錄可辨認出 LightRAG 對照區塊；該區塊列出四個領域與一個平均欄，平均 Diversity win rate 為 ReGraphRAG 92.4%、LightRAG 7.6%。這是 LLM 評審下的相對偏好比例，不是 accuracy、retrieval recall 或跨實驗可比的絕對品質分數；作者摘要概括為平均 Diversity win rate >80%。Table 1 其他比較基線的完整分塊與各維度數值、評審設定、模型與樣本數仍待讀取 PDF 核驗；不從搜尋摘錄推補。[官方 PDF 索引，§5.1、Table 1，約 pp. 5431–5433]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
作者在 Limitations 段指出兩項限制：其 query-aware reranking 以 edge embedding 與 query representation 的 cosine similarity 為基礎，消融中移除此步驟有時反而提升表現，顯示目前分數可能未充分捕捉圖結構的多跳推理能力；Perspective Expansion 會增加子查詢數量，帶來額外檢索與推論時間，可能不適合即時或資源受限環境。重組錯誤邊的風險、完整成本數字及其他限制待核全文。Table 1 的 win rate 不能與 answer accuracy 直接比較。[官方 PDF 索引，Limitations，末頁]

## 對本專案研究領域的實際意義 (Implications for Research Domains)
目前暫列 D04 主域（圖組織／表示）、D03 次域（抽取後圖整理）、D05 次域（查詢時子查詢與 reranking）。由於方法在 query time 重組已檢索子圖，主域也可能應移至 D05；待讀完整方法與系統流程圖後，依 repo「Domain = lifecycle / system research problem」規則重審，不把這個 mapping 說成作者定義。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 官方 entry／metadata／摘要](https://aclanthology.org/2025.findings-emnlp.290/)，DOI [10.18653/v1/2025.findings-emnlp.290](https://doi.org/10.18653/v1/2025.findings-emnlp.290)。
- [ACL 官方 PDF](https://aclanthology.org/2025.findings-emnlp.290.pdf)（PDF 索引可檢索部分正文；本地 PDF 下載逾時，尚無本地副本或頁面截圖）。
- [Hanyang ScholarWorks 機構典藏記錄](https://hanyang.scholarworks.kr/item/a81fc59c-c9f6-4dce-bb69-f32f035fb991)（核對作者、DOI、venue、發表年月與頁碼；僅提供摘要）。
- [作者公開程式庫](https://github.com/ToBeSuperior/ReGraphRAG)（程式碼可用性來源，不作為實驗結果的替代證據）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings NAACL 2025-04) GRAG - Graph Retrieval-Augmented Generation|GRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2025-11) PropRAG - Guiding Retrieval with Beam Search over Proposition Paths|PropRAG]]。
