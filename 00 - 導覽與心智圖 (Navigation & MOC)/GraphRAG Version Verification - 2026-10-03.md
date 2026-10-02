---
title: "GraphRAG Version Verification — 2026-10-03"
tags: [literature-audit, graph-rag, version-verification]
last_updated: "2026-10-03"
audit_scope: "CatRAG Traversal, KAG, M3-Embedding; follow-up to the 44-paper supplementation review"
review_mode: "single-agent; edition-scoped primary-source text comparison and local PDF visual checks"
taxonomy_version: "v2"
---

# CatRAG、KAG、M3 的版本核對

這輪已將 CatRAG 和 M3 的正式全文指定證據與本地預印本比較，修正筆記錯誤並補上正式版內容；KAG 正式全文仍未取得，僅完成書目再核與本地表格抽查。這是 [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Supplementation Review - 2026-10-02|44 篇補齊成果複核]] 的後續，不宣稱其餘論文的出版版也已查完。

## 版本與查核範圍

| 論文 | 本地 PDF | 正式版 | 本輪可確認的範圍 |
|---|---|---|---|
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2026-07) Breaking the Static Graph - Context-Aware Traversal for Graph-Based RAG\|CatRAG Traversal]] | arXiv:2602.01965v1；13 頁 | Findings ACL 2026；5849–5863；15 頁 | 官方 PDF 可抽取文字：題名／作者、核心方法、Tables 1–8、效率／限制、新增案例與 prompts 的文字；本地 v1 Table 2–4 視覺抽查。正式版圖像與逐符號公式比較未完成。 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) M3-Embedding - Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation\|M3-Embedding]] | arXiv:2402.03216v5；2025-12-12；18 頁 | Findings ACL 2024；2318–2335；18 頁 | 官方 PDF 可抽取文字：封面、§2–4、Tables 1–15、Limitations、Appendix B。抽取的表格數值序列相符，人工核對主要分數與訓練條件；本地 Tables 1、5–6／Limitations 視覺核對。References 未逐條完成來源核驗。 |
| [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation\|KAG]] | arXiv:2409.13731v3；33 頁；19 作者 | WWW Companion 2025；334–343；10 頁；12 作者 | 出版社 DOI deposit 再核；本地 Tables 8–9、11 視覺抽查。正式版方法、實驗與附錄差異仍待全文。 |

正式書目／全文依 [CatRAG ACL 紀錄與 PDF (2026/07)](https://aclanthology.org/2026.findings-acl.290/)、[M3 ACL 紀錄與 PDF (2024/08)](https://aclanthology.org/2024.findings-acl.137/)、[KAG ACM DOI deposit（2026-10-03 查閱）](https://api.crossref.org/works/10.1145/3701716.3715240)。頁數按正式頁碼區間及官方 PDF 解析資訊核對；它們不是三篇內容等長或相同的證明。

ACL 官方 PDF 的文字透過遠端 PDF 讀取工具取得；直接 binary 下載仍逾時，未新增本地正式版 PDF。KAG 的 ACM PDF／EPDF／全文端點無法取得；Semantic Scholar DOI record 所回傳的全文是 33 頁 arXiv v3／19 作者，沒有充當 10 頁正式版。原有三份 PDF、路徑、`source_version`、`verified_version`、頁數與 SHA-256 均保留；CatRAG／M3 新增 `additional_verified_versions`，明示正式版證據範圍。`verified` 只指指定版本中筆記記錄的證據，不是所有版本的全面核驗。

## CatRAG：正式版有新增實驗，不能只換題名

- **題名／作者：** v1 題名末段為 *for Robust Retrieval-Augmented Generation*，正式版為 *for Graph-Based RAG*；七位作者及順序相同。[arXiv v1 (2026/02), title page](https://arxiv.org/abs/2602.01965v1)；[正式全文 (2026/07), p. 5849](https://aclanthology.org/2026.findings-acl.290.pdf)
- **方法與附錄：** symbolic anchoring、query-aware edge weighting、passage enhancement 均已在 v1 存在。正式 §3.3.3 更明確界定 fine-grained scoring 只作用於 coarse pruning 後的 top-K edges。Appendix A 的 hyperparameters／tiered projection 數值相符（v1 Tables 6–7 → 正式 Tables 7–8）；正式版新增 Appendix B 的兩個 MuSiQue 案例，prompts 改列 Appendix C／Tables 9–10。案例不是新增大規模 benchmark。[正式全文 (2026/07), §3／Appendices A–C, pp. 5851–5853、5860–5863](https://aclanthology.org/2026.findings-acl.290.pdf)
- **實驗擴充：** Tables 2–5 的共有行數值相符；正式 Tables 2–4 新增 PropRAG，Table 3 新增 HyperGraphRAG。LightRAG 在 v1 和正式版 QA 表都已比較；原文因輸出不直接對應 passage retrieval，未列其 Recall／FCR／JSR。PropRAG 的 MuSiQue QA F1 為 46.1，高於 CatRAG 45.0；HotpotQA Recall@5 為 90.0，高於 CatRAG 89.5。因此不能寫 CatRAG 全面勝出。[正式全文 (2026/07), Tables 2–5, pp. 5855–5856](https://aclanthology.org/2026.findings-acl.290.pdf)
- **新增效率證據：** Table 6／§6.2，MuSiQue 1,000 queries、GPT-4o-mini 下，HippoRAG 2／CatRAG 每 1,000 queries API cost 為 $0.50／$2.00，dynamic weighting 額外階段為 4.65s。另一行標作 `w/o E_rel weighting`、列值 2.92s／7.73s，正文稱約 2.6 倍較慢；筆記保留原標籤及解讀疑點，不擅自稱總端到端延遲。此為歷史 API 費率，未報完整建圖成本、GPU／記憶體、TTFT／吞吐量。[正式全文 (2026/07), Table 6／footnote 3, p. 5857](https://aclanthology.org/2026.findings-acl.290.pdf)
- **原文矛盾：** §6.1 寫 HoVer JSR 相對增幅 11%；§5／§6.2 寫 18.7%。由 Table 4 的 31.1／26.2 計算為 `(31.1 − 26.2) / 26.2 ≈ 18.7%`，已明示這是筆記計算。未代作者解釋 11% 的來源。[正式全文 (2026/07), Table 4／§5–6, pp. 5855–5857](https://aclanthology.org/2026.findings-acl.290.pdf)
- **程式碼界線：** 正式 Limitations 仍說原始 source code 因 proprietary data policy 無法公開；作者 repo README 的 2026-08-20 release 明示是獨立重現實作。已修正「repo 有公開就等於原始實驗可重現」的潛在誤解。[正式全文 (2026/07), Limitations, p. 5858](https://aclanthology.org/2026.findings-acl.290.pdf)；[作者 repo README（2026-10-03 查閱）, Code Release／Updates](https://github.com/kwunhang/CatRAG)

筆記另修正 Table 3 星號解讀：被標記為引用既有結果的是無 retrieval 的 `None` 行，HippoRAG 2 方法行沒有星號。D05／D13 定位維持，新增 FCR／JSR 證據不等於 D06 retrieve／retry／stop controller。[正式全文 (2026/07), Table 3／§4.3, pp. 5854–5855](https://aclanthology.org/2026.findings-acl.290.pdf)；分類為 repo 的 [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|lifecycle mapping]]。

## M3：主要數值相符，筆記有錯誤與遺漏

| 原筆記問題 | 已修正／補充 |
|---|---|
| MIRACL Sparse 寫成 45.3 | Table 1 為 **53.9**；45.3 是 Table 2 的 MKQA Sparse Recall@100，不是同一 benchmark／metric。 |
| Limitations 標 PDF p. 12 | 正式印刷 p. 2326／PDF p. 9，本地 v5 亦為 p. 9。 |
| 第一作者差異寫成正式 PDF 與 arXiv 不同 | 兩版封面均為 **Jianlv Chen**，ACL 書目頁為 **Jianlyu Chen**。canonical `authors` 沿用索引拼寫，另列 `author_name_note`。 |
| 遺漏附錄訓練硬體 | Appendix B.1：32×A100-40GB／20,000 steps；96×A800-80GB／25,000 steps；24×A800-80GB fine-tuning，約 6,000 steps 是 warm-up。這些資源原本就存在於兩版，並非 2025 才新增。 |
| All 的候選協議過於簡略 | §4.1 是以三種 score 對 Dense top-200 rerank；Dense+Sparse 重排兩個 top-1,000 的聯集。長文件權重與 §4.1 不同，已分開標示。 |
| `benchmark_ids` 放一般研究主題 | 多語／跨語／長文件檢索移入 `research_questions`；IDs 改為 MIRACL、MKQA_retrieval、MLDR、NarrativeQA_retrieval，正文定義 split／metric／retrieval protocol，`dataset_ids` 仍記資料名稱。 |

以上分別核於 [正式全文 (2024/08), Tables 1–2／§4.1–4.3／Limitations／Appendix B.1, pp. 2323–2326、2331](https://aclanthology.org/2024.findings-acl.137.pdf) 及 [ACL 官方書目 (2024/08), author list](https://aclanthology.org/2024.findings-acl.137/)。MIRACL Table 1 與 Limitations 也用本地 v5 的渲染頁視覺核對。

已比較 Tables 1–15 抽取文字內的數值序列，沒有發現表格數值變更；人工核對主要平均值、消融與 Appendix B.1 的硬體條件。表格比較排除了正文、引用年份和欄位下標造成的抽取差異，**不包含曲線、圖像 pixel 或逐字 bibliography 核驗**。正式版和 v5 確有引用／書目差異，例如 §4.2 的 BEIR 引用在 v5 顯示 `(?)`，正式版為 Thakur et al. (2021)；因此「表格相符」不能改寫成「全文相同」。[正式全文 (2024/08), §4.2／Tables 1–15／References, pp. 2323–2335](https://aclanthology.org/2024.findings-acl.137.pdf)；[arXiv v5 (2025/12), PDF p. 7](https://arxiv.org/abs/2402.03216v5)

新增 Table 11 邊界提醒：MLDR 的 BM25 Lucene Analyzer 為 64.1，M3 Sparse 為 62.2；主表 BM25 的 XLM-R tokenizer 為 53.6。比較結論須固定 tokenizer 與協議；embedding retrieval 品質與 GPU 訓練配置也不能推導端到端 RAG 服務效率。D04／D05 定位維持。[正式全文 (2024/08), Table 11, p. 2333](https://aclanthology.org/2024.findings-acl.137.pdf)

## KAG：保留未完成的正式版比對

再核 DOI deposit 的 12 位正式作者、334–343 頁及 2025-05-08 出版日期；會議為 2025-04-28 至 05-02，故本地檔名的 2025-04 表示會議起始月份，不是主張出版日期為四月。19 位 preprint 作者仍另存 `preprint_authors`。候選頁先前將 `authors`／`published_authors` 欄位含義寫反，也已對齊實際 YAML。[ACM DOI deposit（2026-10-03 查閱）, authors／page／published](https://api.crossref.org/works/10.1145/3701716.3715240)；[會議官方歷史頁, WWW 2025 日期](https://thewebconf.org/)

本地 Table 8 的 DeepSeek-V2 主結果與筆記一致；但 Table 9 的 KAG MuSiQue Recall@5 為 **65.7**，Table 11 的 `K_Alignment + LFSH_ref3` 為 **65.6**。兩表的 HotpotQA／2Wiki 均為 88.8／91.9，差異成因未核。已按原表分開保留，沒有宣稱正式版也含此差異或已修正。[arXiv v3 (2024/09), Tables 8–9、11, PDF pp. 18、20](https://arxiv.org/abs/2409.13731v3)

`version_comparison_status: published_full_text_unavailable` 與 `published_pdf_last_attempt: 2026-10-03` 只記錄這次結果；不將文獻查詢工具返回的預印全文登記成正式版。後續需要取得對應 DOI 的 10 頁正式全文，才能比對哪些模組、實驗與附錄被保留／刪減。

## 檢查與後續缺口

- 三篇原有 YAML 欄位保留；七板塊、D01–D14／paradigm 字典與本地 PDF 關聯重新檢查。未新增／改寫 PDF binary，庫內仍為 221 篇 paper records、173 個 PDF。
- 本輪重跑 44 篇的 metadata／七板塊、全庫識別碼查重、PDF stamp／頁數／hash，以及 683 條本地連結，未發現問題。額外確認三篇原有 metadata keys 與 edition／hash／domain 欄位保留、Markdown fences 成對；`git diff --check` 通過。這些結構檢查不替代其餘論文的正文核驗。
- 同步 44 篇候選頁、文獻索引及前次複核報告的 CatRAG／M3 正式版閱讀狀態；KAG 仍待正式全文。29 份本地 arXiv 中的 21 篇有正式 metadata，現在其中 **5 篇**另核過正式全文指定證據（GeAR、HybGRAG、StructGPT、CatRAG、M3），不代表這 5 篇全部版本差異均完成。
- 剩餘工作優先核 KAG 正式全文與其他已有出版 metadata 的版本；GFM-RAG 既有 anchor 的七板塊／本地 PDF 缺口仍保留在前次報告，這輪未擴大範圍處理。Domain-level survey coverage 仍由 [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]] 集中維護。

此輪沒有改變 domain 定義、提出新的 paradigm，或將未核資訊升為 survey 共識；分類只依已核機制對齊現有 taxonomy。
