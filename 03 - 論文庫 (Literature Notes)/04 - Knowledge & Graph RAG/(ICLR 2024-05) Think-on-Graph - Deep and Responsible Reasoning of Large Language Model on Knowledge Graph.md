---
paper_id: "Sun2024_ThinkOnGraph"
title: "Think-on-Graph: Deep and Responsible Reasoning of Large Language Model on Knowledge Graph"
authors:
  - "Jiashuo Sun"
  - "Chengjin Xu"
  - "Lumingyuan Tang"
  - "Saizhuo Wang"
  - "Chen Lin"
  - "Yeyun Gong"
  - "Lionel M. Ni"
  - "Heung-Yeung Shum"
  - "Jian Guo"
year: 2023
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2307.07697"
url: "https://proceedings.iclr.cc/paper_files/paper/2024/hash/10a6bdcabbd5a3d36b760daa295f63c1-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph.pdf"
tags:
  - paper
  - kgqa
  - graph-traversal
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D12"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "kg_path_search"
  - "retrieval_efficiency"
benchmark_ids:
  - "CWQ"
  - "WebQSP"
  - "GrailQA"
  - "QALD10-en"
dataset_ids:
  - "CWQ"
  - "WebQSP"
  - "GrailQA"
  - "Simple Questions"
  - "WebQuestions"
  - "T-REx"
  - "Zero-Shot RE"
  - "Creak"
metrics:
  - "Hits@1"
---

# Think-on-Graph: Deep and Responsible Reasoning of Large Language Model on Knowledge Graph

> **版本與來源：** arXiv 首次發布於 2023 年；本筆記及本地 PDF 對應 ICLR 2024 正式版。方法與數字均按正式 proceedings 全文整理。

## 一話摘要 (TL;DR)
ToG 讓 LLM 在知識圖譜上逐輪進行 beam search，透過關係與實體探索取得可追溯推理路徑，再以路徑回答問題。

## 研究背景與問題定義 (Problem Statement)
作者指出，單靠 LLM 容易受過時或缺漏的參數知識影響；只把 KG 當外部資料庫、由 LLM 產生查詢的鬆散整合，也會受 KG 覆蓋不足限制。ToG 研究的是如何讓 LLM 參與 KG 搜尋過程，藉動態探索與模型既有知識互補。範圍主要是 KGQA 與知識密集任務，不等同於從任意文件即時建圖的 GraphRAG pipeline。[pp. 1–3, §1–2]

## 核心方法與技術架構 (Methodology & Architecture)
1. **初始化：** LLM 從問題辨識 topic entities，形成初始 beam。
2. **探索：** 每一輪先以 KG 查詢取得候選關係，由 LLM 依問題裁剪，再依選中的關係查詢候選實體並裁剪，更新前 N 條推理路徑。
3. **判斷與回答：** LLM 檢查目前路徑是否足以回答；若足夠則根據路徑生成答案，否則繼續搜尋至最大深度。論文另提出 ToG-R，以 relation chain 搜尋並隨機裁剪候選實體，減少 LLM 呼叫。

搜尋寬度及最大深度均設為 3；論文給出 ToG 最多約 `2ND + D + 1` 次 LLM 呼叫、ToG-R 最多約 `ND + D + 1` 次的上界。[pp. 3–5, §2]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 6：** 在 CWQ、WebQSP、GrailQA、QALD10-en、Simple Questions、WebQuestions、T-REx、Zero-Shot RE、Creak 九個資料集上以 Hits@1 評估。GPT-4 + ToG 在六個資料集優於論文列出的既有 SOTA；例：WebQSP 82.6、GrailQA 81.4、Creak 95.6。GrailQA 與 Simple Questions 各隨機抽 1,000 筆作測試，與完整測試集結果不可混看。
- **Table 2, p. 6：** CWQ / WebQSP 上，GPT-4 + ToG 相對 GPT-4 CoT 分別為 69.5 vs. 46.0、82.6 vs. 67.3 Hits@1；模型與任務限定於該表設定。
- **設定：** Freebase 用於多數資料集，QALD10-en、T-REx、Zero-Shot RE、Creak 使用 Wikidata；beam 寬度與最大深度為 3、生成上限 256 tokens。Llama-2-70B-Chat 使用 8 張 A100-40G、未量化；ChatGPT/GPT-4 透過 OpenAI API 呼叫。文中未提供可直接與其他工作對齊的端到端延遲或硬體總成本。[§3.1–3.2, pp. 5–8]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 顯式路徑提供可檢查的 KG 證據；LLM 可在搜尋中依自然語言相關性選擇關係／實體，不需另訓練檢索器。ToG-R 降低裁剪階段 LLM 呼叫數。
- **限制與代價：** 反覆提示造成多次 LLM 呼叫；效能依賴 topic entity linking、KG 覆蓋與候選分枝品質。達到最大搜尋深度仍不足時，系統會退回 LLM 內部知識作答，答案不再完全由 KG 路徑支持。測試包含抽樣資料集，API 模型版本和今日服務亦不可視為完全相同條件。[§2.1.3、§3.1.3、§3.2, pp. 5–9]
- **比較邊界：** Table 1 同時列出 fine-tuned 與 prompting 系統；訓練資料、模型、資料集切分不完全一致。作者亦指出若基準方法不是相同 exact-match 設定則不比較；不應將該表視為同資源成本排名。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本筆記將 ToG 定位於 **D05 Query Understanding & Retrieval**，D12 為次領域，因 LLM 直接控制圖 traversal 與停止／繼續搜尋；使用 `graph_rag`、`multi_hop_rag`。這是 repo taxonomy mapping，不是作者原有分類。與文件圖譜建立型方法相比，ToG 假設已有可查詢 KG，可作為 query-time graph retrieval / agentic traversal 的對照案例。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式全文：[ICLR 2024 proceedings PDF](https://proceedings.iclr.cc/paper_files/paper/2024/file/10a6bdcabbd5a3d36b760daa295f63c1-Paper-Conference.pdf)；[arXiv:2307.07697](https://arxiv.org/abs/2307.07697)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning|RoG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation|SubgraphRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) GraphReader - Building Graph-based Agent to Enhance Long-Context Abilities of Large Language Models|GraphReader]]。
