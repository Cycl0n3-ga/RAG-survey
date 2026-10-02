---
paper_id: "Xiao2026_LogicPoison"
title: "LogicPoison: Logical Attacks on Graph Retrieval-Augmented Generation"
authors: ["Yilin Xiao", "Jin Chen", "Qinggang Zhang", "Yujing Zhang", "Chuang Zhou", "Longhao Yang", "Lingfei Ren", "Xin Yang", "Xiao Huang"]
year: 2026
publication_year: 2026
venue: "Proceedings of the 64th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)"
doi: "10.18653/v1/2026.acl-long.252"
arxiv: "2604.02954"
url: "https://aclanthology.org/2026.acl-long.252/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-04) LogicPoison - Logical Attacks on Graph Retrieval-Augmented Generation.pdf"
tags: ["paper", "graph-poisoning", "security-attack"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains: ["D04", "D05"]
paradigm_tags: ["graph_rag"]
adjacent_interfaces: []
research_questions: ["graph_topology_attack", "knowledge_base_poisoning", "multi_hop_failure", "graph_rag_defense"]
benchmark_ids: ["HotpotQA", "2WikiMultiHopQA", "MuSiQue"]
dataset_ids: ["HotpotQA", "2WikiMultiHopQA", "MuSiQue"]
metrics: ["Attack Success Rate", "ASR-GPT", "Attack Time", "Token Cost"]
---

# LogicPoison: Logical Attacks on Graph Retrieval-Augmented Generation

> **版本界線：** ACL 2026 正式論文頁、DOI、作者與頁碼已核對；本地全文是 arXiv v1（2026-04-03），正式版 PDF 下載端點本次逾時，正式版修改尚待比對。以下數據依 arXiv v1 頁碼。

## 一話摘要 (TL;DR)
LogicPoison 以同型實體置換破壞 GraphRAG 知識圖譜中的邏輯連邊，研究即使表面文字合理、圖拓樸已被污染時，系統仍可能遭受的檢索與推理攻擊。

## 研究背景與問題定義 (Problem Statement)
傳統 RAG 攻擊常注入惡意文件或指令，但 GraphRAG 會從文字抽取實體、關係和社群，局部雜訊不一定影響其推理路徑。作者研究更隱蔽的攻擊面：改寫同類型實體名稱，使文本仍可讀，卻令索引後的圖連結與 gold reasoning chain 錯位。[§1–3, arXiv v1 pp. 1–4]

## 核心方法與技術架構 (Methodology & Architecture)
攻擊分兩路：Global Logic Poison 選擇高中心性／頻率的 hub，Query-Centric Logic Poison 從問題推導必要的 bridge entities；再在相同 entity type 內作 cyclic permutation，重寫語料中的實體提及而不改 query 或 gold answer。重新建圖後，原推理路徑可能被導向 dead end 或錯誤捷徑。論文亦測試 query paraphrasing 作為防禦。[§3–5, pp. 3–7]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv v1 p. 5：** GPT-4o-mini、HotpotQA 條件下，LogicPoison 對 Microsoft GraphRAG 的 ASR / ASR-GPT 為 78.4 / 92.2，對 HippoRAG2 為 73.6 / 66.2；ASR 以 gold string 缺席計算，ASR-GPT 以 judge 判語義等價，兩者不可混讀。每資料集抽樣 500 個 validation queries。
- **Table 2, p. 6：** 在 2Wiki 上 GPT-4o-mini 對 GraphRAG ASR / ASR-GPT 為 78.4 / 95.6，對 GFM-RAG 為 71.6 / 76.0；這是 attack success，不是正常效能指標。
- **Table 3, p. 7：** 三資料集平均，LogicPoison 時間成本 1,406.4 秒、token 成本 74.9；PoisonedRAG 分別 6,607.3 秒、593.6。文中表示 LogicPoison 不需在語料加入 attack tokens。
- **設定：** HotpotQA、2WikiMultiHopQA、MuSiQue 各抽 500 query；GeForce RTX 5090、Facebook/contriever embedding、retrieval top-k=10、target entity top-n=5%；base LLM 為 GPT-4o-mini、Llama-3.1-8B、Qwen-3-32B。[§5.1–5.4, pp. 5–7]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **研究貢獻：** 指出 graph topology、實體消歧與多跳 bridge 的完整性屬於安全邊界，補足只討論 prompt injection 或插入錯誤文件的攻擊模型。
- **限制與代價：** 評測限三個多跳 QA benchmark、三種 GraphRAG 系統和指定抽樣；攻擊依賴實體型別辨識與語料可重寫，未證明對所有 GraphRAG/知識來源都同樣有效。提出的 query paraphrasing defense 幾乎沒有降低本文設定中的 ASR，不能外推為對其他防禦無效。
- **安全邊界：** 表列 ASR 高低依賴 answer string / LLM judge 定義；僅在同一 dataset、模型、graph pipeline 和攻擊預算下比較。請將此文視為威脅模型與失效證據，不是所有 GraphRAG 固有不安全的結論。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
歸入 **D14 RAG Systems, Security & Privacy**，次領域 D04/D05。它補上圖譜拓樸完整性、實體映射與攻擊後多跳召回的測試軸，並可連結 D13 的 attack success / failure attribution；分類本身不代表本文已提供完整防禦方案。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 正式論文頁、DOI 與頁碼](https://aclanthology.org/2026.acl-long.252/)；[arXiv:2604.02954 v1（2026-04-03，全文）](https://arxiv.org/abs/2604.02954)。ACL 正式版發表於 2026-07，頁 5575–5591。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-04) LogicPoison - Logical Attacks on Graph Retrieval-Augmented Generation.pdf|開啟本地 arXiv v1 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GNN-RAG - Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs|GNN-RAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(AAAI 2026-03) PathRAG - Pruning Graph-Based Retrieval Augmented Generation with Relational Paths|PathRAG]]。
