---
paper_id: "Lee2025_HybGRAG"
title: "HybGRAG: Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases"
authors: ["Meng-Chieh Lee", "Qi Zhu", "Costas Mavromatis", "Zhen Han", "Soji Adeshina", "Vassilis N. Ioannidis", "Huzefa Rangwala", "Christos Faloutsos"]
year: 2024
publication_year: 2025
venue: "ACL 2025"
doi: "10.18653/v1/2025.acl-long.43"
arxiv: "2412.16311"
url: "https://aclanthology.org/2025.acl-long.43/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases.pdf"
tags: ["paper", "hybrid-question-answering", "semi-structured-knowledge-base"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: ["D12", "D04", "D07"]
paradigm_tags: ["graph_rag", "hybrid_rag", "adaptive_rag", "reflective_rag"]
adjacent_interfaces: []
research_questions: ["hybrid-text-graph-retrieval", "question-routing", "critic-guided-retrieval-refinement"]
benchmark_ids: ["STaRK", "CRAG"]
dataset_ids: ["STaRK-MAG", "STaRK-PRIME", "CRAG"]
metrics: ["Hit@1", "Hit@5", "Recall@20", "MRR"]
source_version: arXiv:2412.16311v2
verified_version: arXiv:2412.16311v2
pdf_pages: 15
pdf_sha256: 34a144419fb2069abc1faeebeef2126b80d61f8804cfee182edbaada139dd343
additional_verified_versions:
  - "ACL 2025 (method, Tables 2–7, appendices, Limitations)"
---

# HybGRAG: Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases

> **版本與閱讀範圍：** 已讀 ACL Anthology ACL 2025 正式全文（15 頁），DOI `10.18653/v1/2025.acl-long.43`；另可用全文副本為 arXiv:2412.16311 v2，已核對正式版表 5 的關鍵結果與摘要一致。本地 PDF 為 arXiv v2，故正式版／預印本之細節差異仍以 ACL 正文為準。

## 一話摘要 (TL;DR)
HybGRAG 以 retriever bank 同時處理文本與圖關係檢索，再讓 validator/commenter critic 根據檢索是否符合問題要求修正路由。

## 研究背景與問題定義 (Problem Statement)
半結構化知識庫（SKB）由互相關聯的文本文件和知識圖組成。問題可能同時要求文本語義和圖關係條件；只做 dense text retrieval 會漏關係約束，只做 graph QA 則可能混淆文本語義需求與關係需求。論文把目標明確定為：按 hybrid question 的 relational 和 textual aspects，檢索符合條件的文件集合。[§1–2.1, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
Retriever bank 有 text module（question–document vector similarity search）和 hybrid module。後者由 router 抽 topic entities／useful relations，在 KG ego-graph 中取關聯 entities，再以文本相似度排序所連文件。Critic 將「是否符合問題」拆為 validator（二元驗證，使用圖上的 reasoning paths 作 context）及 commenter（針對錯誤實體、關係、交集或 retrieval module 產生具體 corrective feedback）；router 依 feedback 重新抽取並重試。這把圖邊用作可檢查的關係條件，把文本 embedding 用作內容排序。[§3, pp. 3–5; Algorithm 1]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 5, p. 6：** STaRK-MAG／STaRK-PRIME test set 分別 2,665／2,801 題；資料庫為學術 KG／精準醫療 KG，且各有與 entity 關聯的文件。HybGRAG Hit@1 為 0.6540／0.2856，Hit@5 為 0.7531／0.4138，Recall@20 為 0.6570／0.4358。相對表內最佳非自身 baseline，Hit@1 增幅分別 47.4%／54.9%。Think-on-Graph 等高成本方法僅評估 10% test questions，表中以星號標示，這點需保留在比較解讀中。
- **Table 2–3, p. 3：** STaRK-MAG 上單獨 text VSS、graph PPR 的 Hit@1 各為 0.2908、0.2533；oracle optimal routing 為 0.4522，顯示兩種信號在該資料集能提供互補正確例，但 oracle 不是可部署系統分數。Table 3 又顯示以 corrective feedback 的 2-iteration extraction hit rate 為 0.9231，而初次抽取是 0.6769。
- **Table 6–7, p. 6：** STaRK-MAG 改 Claude 3 Haiku 時 Hit@1 0.6019、MRR 0.6483；`Hybrid RM` 無 agent 為 0.5028 Hit@1，single-agent router 為 0.6206，完整 HybGRAG 為 0.6540。CRAG 在附錄測試的是 end-to-end generation，與 STaRK retrieval 表分開呈現。
- **模型／資源：** 主實驗使用 Claude 3 Sonnet router/critic 及 `text-embedding-ada-002` 等實作元件；附錄描述 STaRK retrieval 和 CRAG generation。作者指出部分 baseline 延遲與費用高，只取 10% 測試題；沒有提供可泛化到其他硬體/API 的完整成本表。[§4, pp. 5–7; Appendix A–C, pp. 10–14]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 針對「同時需要內容和圖關係」的明確 hybrid QA 情境，不假定單一 retriever 可解所有 query；critic 把路由錯誤拆成具體可修正類型。實驗另外展示 no-agent、single-agent 及小模型消融。
- **限制與代價：** 多個 LLM 呼叫（router、validator、commenter）可能增加 latency/API 成本；驗證仰賴 LLM judge/validation context 及資料庫 schema，且可修正次數有限。STaRK 只用 MAG 與 PRIME 兩個資料子集（因法律原因），不能視作所有領域 HQA 的代表；圖的 entity/relation schema 需已可用。
- **比較邊界：** Table 5 對比是 STaRK retrieval，不等同端到端回答品質；作者在 CRAG 上另測回答。不同資料庫、baseline evaluation fraction、LLM/API 及 metric 不同時，不可據此宣稱對一般 Vector RAG 或 GraphRAG 無條件更好。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸入 **D05 Query Understanding & Retrieval**：主要問題是依 query 選擇／聯合 retriever 並排序文件。D12 表示 critic 觸發路由修正的 action loop，D04 表示 KG retrieval 結構，D07 表示被取回文件集合；標籤用 `adaptive_rag`、`reflective_rag` 及 `hybrid_rag`。本篇提供 LightRAG 等圖式 RAG 以外的另一比較軸：不是只問圖怎麼建或 traversal，而是混合 knowledge base 的 query routing 及回饋控制。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology ACL 2025](https://aclanthology.org/2025.acl-long.43/)；[DOI 10.18653/v1/2025.acl-long.43](https://doi.org/10.18653/v1/2025.acl-long.43)；[arXiv:2412.16311 v2](https://arxiv.org/abs/2412.16311)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2023-12) StructGPT - A General Framework for Large Language Model to Reason over Structured Data|StructGPT]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation|KAG]]。
