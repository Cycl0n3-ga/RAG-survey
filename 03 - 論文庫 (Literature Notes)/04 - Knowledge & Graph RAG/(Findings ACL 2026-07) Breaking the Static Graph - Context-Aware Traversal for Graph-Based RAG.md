---
paper_id: "Lau2026_CatRAGTraversal"
title: "Breaking the Static Graph: Context-Aware Traversal for Graph-Based RAG"
authors: ["Kwun Hang Lau", "Fangyuan Zhang", "Boyu Ruan", "Yingli Zhou", "Qintian Guo", "Ruiyuan Zhang", "Xiaofang Zhou"]
year: 2026
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.290"
arxiv: "2602.01965"
url: "https://aclanthology.org/2026.findings-acl.290/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) Breaking the Static Graph - Context-Aware Traversal for Robust Retrieval-Augmented Generation.pdf"
tags: ["paper", "query-aware-traversal", "reasoning-completeness"]
verification_status: "verified"
last_verified: "2026-10-03"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: ["D13"]
paradigm_tags: ["graph_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["query_aware_graph_traversal", "evidence_chain_completeness", "retrieval_evaluation"]
benchmark_ids: ["MuSiQue", "2WikiMultiHopQA", "HotpotQA", "HoVer"]
dataset_ids: ["MuSiQue", "2WikiMultiHopQA", "HotpotQA", "HoVer"]
metrics: ["Recall@5", "F1", "Accuracy", "Full Chain Retrieval", "Joint Success Rate"]
source_version: arXiv:2602.01965v1
verified_version: arXiv:2602.01965v1
pdf_pages: 13
pdf_sha256: 3f2e11df25502a75d5e7ba240acb2e69e37e453c5845d959d595272280199f14
source_title: 'Breaking the Static Graph: Context-Aware Traversal for Robust Retrieval-Augmented
  Generation'
additional_verified_versions:
  - "Findings ACL 2026 (official PDF text: title/authors, Sections 3–6, Tables 1–8, Limitations, Appendices B–C)"
version_comparison_status: "scoped_text_comparison"
---

# Breaking the Static Graph: Context-Aware Traversal for Graph-Based RAG

> **版本界線：** 本地 PDF 保留 arXiv v1（2026-02-02，13 頁），預印題名為 *Breaking the Static Graph: Context-Aware Traversal for Robust Retrieval-Augmented Generation*。2026-10-03 已讀 ACL 官方 PDF 的可抽取文字並與 v1 比較：正式版為 Findings ACL 2026，頁 5849–5863（15 頁），七位作者與順序相同；增加 PropRAG／HyperGraphRAG 基線、§6.2 效率分析及 Appendix B 案例。下述正式版表格採印刷頁碼，另註 PDF 頁碼。官方 PDF binary 未保存本地，正式版圖像未作視覺核對，不宣稱整份檔案或所有公式逐符號相同。詳見 [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Version Verification - 2026-10-03|版本核對報告]]。[正式全文 (2026/07), pp. 5849–5863](https://aclanthology.org/2026.findings-acl.290.pdf)

## 一話摘要 (TL;DR)
CatRAG 在 HippoRAG 2 的 PPR 圖檢索上加入 symbolic anchoring、query-aware dynamic edge weighting 和 key-fact passage enhancement，以補齊多跳證據鏈。

## 研究背景與問題定義 (Problem Statement)
靜態圖檢索的 edge weight 在索引時固定，可能忽略 query-specific relevance，使隨機漫步偏向高 degree hub，造成部分 recall 尚可但完整推理鏈缺失。本文研究 traversal 時如何調整 query-conditioned navigation，並以 evidence-chain completeness 補充一般 recall 指標。[§1–3, arXiv PDF pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
1. **Symbolic anchoring：** 以弱 entity constraints 引導 random walk。
2. **Query-aware dynamic edge weighting：** 由 LLM 評估邊與 query 的相關性，動態調整 traversal 權重。
3. **Key-fact passage enhancement：** 對可能包含關鍵事實的來源 passage 加權。

最後用 PPR 排序 passages，再交給 Llama reader。三個核心模組在兩版均存在；正式版 §3.3.3 明確說明 fine-grained LLM scoring 僅作用於 coarse pruning 後留下的 top-K edges。Appendix A 的八項 hyperparameters 與 tiered edge-weight projection 數值亦相同：原 Tables 6–7 改編為正式 Tables 7–8。這裡的 reasoning completeness 是評估完整取回鏈的能力，不等於 D06 的充分性判定或 retry/stop controller。[正式全文 (2026/07), §3–4／Appendix A, pp. 5851–5854、5860](https://aclanthology.org/2026.findings-acl.290.pdf)

## 主要實驗結果與證據 (Empirical Results & Evidence)
**設定：** GPT-4o-mini 作 LLM 元件，text-embedding-3-small 作 retriever，Llama-3.3-70B-Instruct 作 reader，使用 top-5 passages；作者稱結構方法採相同 extractor/retriever。四資料集各抽 1,000 queries／claims，corpus passages 依序為 11,656／6,119／9,811／9,440；不是完整資料集上的成績。未提供統一 reader context token budget。[正式全文 (2026/07), §4／Table 1, pp. 5853–5854](https://aclanthology.org/2026.findings-acl.290.pdf)

兩版共有行的 Tables 2–5 數值相符；正式版新增行如下。每個欄位的順序均為 MuSiQue／2Wiki／HotpotQA／HoVer。[正式全文 (2026/07), Tables 2–5, pp. 5855–5856（PDF pp. 7–8）](https://aclanthology.org/2026.findings-acl.290.pdf)

| 方法 | Recall@5（Table 2） | QA F1／HoVer accuracy（Table 3） |
|---|---|---|
| CatRAG | 64.9／87.0／89.5／76.8 | 45.0／69.7／71.4／69.0 |
| HippoRAG 2 | 61.4／85.9／87.1／71.2 | 43.2／68.1／69.4／67.2 |
| LightRAG | 原表不列 passage retrieval 結果 | 43.0／49.7／68.3／66.5 |
| HyperGraphRAG（正式版新增） | 原表不列 passage retrieval 結果 | 44.8／61.7／69.5／67.0 |
| PropRAG（正式版新增） | 61.8／83.5／90.0／71.9 | 46.1／63.9／71.2／66.9 |

- **Table 4：** FCR 是 gold supporting documents 全部命中的 query 比例；JSR 同時要求 FCR 與正確答案。CatRAG 的 FCR／JSR 為 34.6／24.3、67.6／55.0、80.4／56.8、42.5／31.1；HippoRAG 2 為 30.5／21.5、66.1／53.0、75.5／53.4、34.8／26.2。新增 PropRAG 為 33.8／24.5、62.8／50.8、81.0／58.2、34.9／25.6。CatRAG 並非每個指標／資料集最高，例如 PropRAG 的 MuSiQue QA F1、HotpotQA Recall@5／FCR／JSR 較高。[正式全文 (2026/07), §4.3／Table 4, pp. 5854–5855](https://aclanthology.org/2026.findings-acl.290.pdf)
- **Table 5：** 三個模組消融保持原數值；移除 passage enhancement 的 2Wiki Recall@5 為 88.4，高於完整方法 87.0，不應寫成各模組在所有資料集均有增益。[正式全文 (2026/07), Table 5, p. 5856](https://aclanthology.org/2026.findings-acl.290.pdf)
- **正式版新增 Table 6／§6.2：** MuSiQue 1,000 queries、GPT-4o-mini 條件下，HippoRAG 2／CatRAG 的 initial seed latency 為 2.75s／2.86s；dynamic edge weighting 為 N/A／4.65s；API cost 為每 1,000 queries $0.50／$2.00。另一延遲行原標籤為 `w/o E_rel weighting`、列值 2.92s／7.73s，但正文把效率代價描述為約 2.6 倍；該行命名與正文關係不清，不擅自改稱總端到端 latency。價格是論文寫作時費率，非現行報價；未報 GPU、記憶體、TTFT、吞吐量或完整 indexing cost。[正式全文 (2026/07), Table 6／footnote 3, p. 5857（PDF p. 9）](https://aclanthology.org/2026.findings-acl.290.pdf)
- **原文不一致：** §6.1 寫 HoVer JSR 相對增幅 11%，§5／§6.2 寫 18.7%；按 Table 4 的 31.1 與 26.2 計算為約 18.7%（本筆記自行計算）。保留矛盾，不將 11% 當作可核結論。[正式全文 (2026/07), Table 4／§5–6, pp. 5855–5857](https://aclanthology.org/2026.findings-acl.290.pdf)

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 同時評估 passage recall、QA、FCR/JSR，避免以部分命中推定完整推理成功；包含模組消融。
- **限制與代價：** Dynamic edge weighting 需 query-time LLM inference；只用 text-embedding-3-small 以隔離拓樸效果，測試 corpus 也是抽樣版本。原始 experimental source code 在正式版仍受 proprietary data policy 限制；2026-10-03 查得作者 repo 的 README 明示 2026-08-20 釋出的是獨立重現實作及 datasets／prompts，不能當作原始實驗程式已公開。[正式全文 (2026/07), Limitations, p. 5858（PDF p. 10）](https://aclanthology.org/2026.findings-acl.290.pdf)；[作者 repo README（2026-10-03 查閱）, Code Release／Updates](https://github.com/kwunhang/CatRAG)
- **比較邊界：** Table 3 的星號標在無 retrieval 的 `None` 行，表示引用 HippoRAG 2 論文的數字；HippoRAG 2 方法行本身沒有星號，不能把兩者混稱。LightRAG 已在 QA 表比較，未列 passage recall／FCR／JSR 是原文輸出形式的限制，不代表分數為零。作者的 “Static Graph Fallacy” 是研究診斷，不是所有固定圖檢索必然失效的證明。新增案例亦不構成醫療／法律部署效果證據。[正式全文 (2026/07), Tables 2–4／Appendix B, pp. 5855、5860–5861](https://aclanthology.org/2026.findings-acl.290.pdf)

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸入 **D05 Query Understanding & Retrieval**，次領域 D13（完整證據鏈評估）。本文沿用 HippoRAG 2 的 corpus graph；query-conditioned transition matrix 與 runtime edge weighting 是 D05 檢索策略，不另當作 D04 corpus-side indexing 貢獻；使用 `graph_rag`、`multi_hop_rag`。這是 repo mapping。它補足 PPR retrieval 的 query-conditioned traversal；不因 “complete evidence chain” 一詞就視為已解決 D06 evidence sufficiency。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 正式紀錄／DOI／頁碼](https://aclanthology.org/2026.findings-acl.290/)；[正式版 PDF（已核可抽取文字）](https://aclanthology.org/2026.findings-acl.290.pdf)；[arXiv:2602.01965 v1](https://arxiv.org/abs/2602.01965v1)；[作者重現實作](https://github.com/kwunhang/CatRAG)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) Breaking the Static Graph - Context-Aware Traversal for Robust Retrieval-Augmented Generation.pdf|開啟本地 arXiv v1 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models|HippoRAG 2]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs|GNN-RAG]]。
