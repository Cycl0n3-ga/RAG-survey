---
paper_id: "Ma2024_ToG2"
title: "Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation"
authors:
  - "Shengjie Ma"
  - "Chengjin Xu"
  - "Xuhui Jiang"
  - "Muzhi Li"
  - "Huaren Qu"
  - "Cehao Yang"
  - "Jiaxin Mao"
  - "Jian Guo"
year: 2024
publication_year: 2025
venue: "ICLR 2025"
doi: null
arxiv: "2407.10805"
url: "https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation.pdf"
tags:
  - paper
  - knowledge-graph
  - multi-hop-reasoning
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D04"
  - "D07"
  - "D09"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "knowledge_graph_and_document_retrieval"
  - "iterative_evidence_retrieval"
  - "evidence_sufficiency_judgment"
benchmark_ids:
  - "WebQSP"
  - "AdvHotpotQA"
  - "QALD10-en"
  - "FEVER"
  - "Creak"
  - "Zero-Shot RE"
  - "ToG-FinQA"
dataset_ids:
  - "WebQSP"
  - "AdvHotpotQA"
  - "QALD10-en"
  - "FEVER"
  - "Creak"
  - "Zero-Shot RE"
  - "ToG-FinQA"
metrics:
  - "Exact Match"
  - "Accuracy"
source_version: ICLR 2025 proceedings
verified_version: ICLR 2025 proceedings
pdf_pages: 25
pdf_sha256: 154e127fd76f802e500e080f4ad8f1f8ca6a7c69c004156ced985fd898ac69fc
---

# Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation

> **版本與閱讀範圍：** arXiv 首發 2024-07，arXiv:2407.10805；本地 PDF 為 ICLR 2025 正式版（25 頁，首頁標示 Published as a conference paper at ICLR 2025）。本筆記依正式版全文與其表格頁碼。

## 一話摘要 (TL;DR)
ToG-2 在知識圖譜搜尋與文件檢索間迭代切換，以圖譜路徑建立線索、以文件片段補充實體語境，並在每輪判斷目前證據是否足以回答。

## 研究背景與問題定義 (Problem Statement)
只靠 KG 路徑可能缺少自由文本細節，只靠文件搜尋則難以連起分散的多跳關係；既有流程也可能在檢索無效時重複擴展。本文研究如何讓圖結構探索與文件 evidence retrieval 互相提供線索，並讓 LLM 在迭代中更新查詢與停止判斷。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
系統先辨識問題中的 topic entities，進行 relation discovery、LLM relation pruning 與 entity expansion；再用候選實體關聯的 Wikipedia chunks 排序，挑選內容作下一輪 topic entities。每輪將 KG triple paths、檢索 chunks 及歷史 clues 提交給 LLM 判斷能否作答；若不足則形成 clues 並重寫查詢，直到足夠或達到深度上限。主要實驗設定為寬度 W=3、最大深度 3；主要 backbone 為 GPT-3.5-turbo，另測 GPT-4o、Llama-3-8B、Qwen2-7B。[§3–4.3, pp. 3–8]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 7：** GPT-3.5-turbo 下，ToG-2 在 WebQSP / AdvHotpotQA / QALD10-en 的 EM 為 81.1 / 42.9 / 54.1，FEVER / Creak 的 Accuracy 為 63.1† / 93.5，Zero-Shot RE 的 EM 為 91.0。FEVER 的 †/‡ 對應不同 few-shot 條件；表中 CoK 的部分數值亦採不同 shot 數，不應忽略其標記作無條件排名。
- **Table 2, p. 7：** ToG-FinQA 的分數為 34.0%，表列 ToG 14.0%、GraphRAG 6.2%、Vanilla RAG 與 CoT 為 0。作者指出 GraphRAG 只在此任務比較，原因是大規模語料索引成本過高；此結果只代表該資料與設定。
- **Table 3, p. 8：** AdvHotpotQA 上 ToG-2 隨 backbone 為 Llama-3-8B 34.7、Qwen2-7B 30.8、GPT-3.5-turbo 42.9、GPT-4o 53.3 EM；模型不同，不能把此列解讀成控制其他條件後的單一模型比較。
- **資源：** 論文列出模型與檢索設定，但未在主要實驗中報告可重現的統一硬體成本／端到端延遲；成本取捨不宜由表中準確率推定。[§4.1–4.3, pp. 6–8]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** KG 提供多跳結構線索，文字片段補充實體語境；迭代 clues 可讓後續檢索帶有先前收集到的上下文；停止判斷把 evidence sufficiency 放進檢索迴圈。
- **限制與成本：** 方法涉及多次 LLM relation selection、文件檢索與生成判斷，推論成本可能隨搜尋輪次增加；寬度與深度需控制候選膨脹。實驗使用 full Wikipedia 與 Wikidata 的設定，不能直接代表所有封閉語料或線上服務成本。論文未提供本文所有設定的硬體／延遲對照。
- **比較邊界：** Table 1 中有 baseline 的 shot 數差異；FinQA 特別比較也不等同於在相同建索引成本下的一般 GraphRAG 比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 分類為 **D05 Query Understanding & Retrieval**，D04 記錄 KG／文件檢索的索引介面，D07 記錄跨輪檢索 evidence 的組織，D09 記錄以累積 evidence 回答。paradigm tags 為 `graph_rag`、`multi_hop_rag`。它可與 ToG 的 KG 搜尋、RoG 的 relation-path planning，以及 SubgraphRAG 的可學習子圖選取並列，區分檢索迴圈是否跨越 KG 與文件兩種知識源。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式全文：[ICLR 2025 論文頁](https://proceedings.iclr.cc/paper_files/paper/2025/hash/830b1abc6d2da85f23d41169fa44d185-Abstract-Conference.html)；[arXiv:2407.10805](https://arxiv.org/abs/2407.10805)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation]]。
