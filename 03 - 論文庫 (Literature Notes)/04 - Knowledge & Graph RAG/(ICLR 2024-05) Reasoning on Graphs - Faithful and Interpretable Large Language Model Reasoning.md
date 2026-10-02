---
paper_id: "Luo2024_ReasoningOnGraphs"
title: "Reasoning on Graphs: Faithful and Interpretable Large Language Model Reasoning"
authors:
  - "Linhao Luo"
  - "Yuan-Fang Li"
  - "Gholamreza Haffari"
  - "Shirui Pan"
year: 2023
publication_year: 2024
venue: "ICLR 2024"
doi: null
arxiv: "2310.01061"
url: "https://proceedings.iclr.cc/paper_files/paper/2024/hash/3e2aeb66481dd63a32421bf032b70384-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning.pdf"
tags:
  - paper
  - kgqa
  - relation-path-planning
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D09"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "relation_path_planning"
  - "faithful_reasoning"
benchmark_ids:
  - "WebQSP"
  - "CWQ"
  - "MetaQA-3hop"
dataset_ids:
  - "WebQSP"
  - "CWQ"
  - "MetaQA-3hop"
metrics:
  - "Hits@1"
  - "F1"
---

# Reasoning on Graphs: Faithful and Interpretable Large Language Model Reasoning

> **版本與來源：** arXiv 首次發布於 2023 年；本筆記使用 ICLR 2024 正式版全文。ICLR 摘要頁作者縮寫為 Reza Haffari；正式 PDF 與 arXiv 作者資料列作 Gholamreza Haffari。

## 一話摘要 (TL;DR)
RoG 先由微調 LLM 產生受 KG 關係詞彙約束的 relation-path 計畫，再檢索有效圖路徑並讓 LLM 根據這些路徑回答，將規劃、檢索與推理分開。

## 研究背景與問題定義 (Problem Statement)
既有 KG 增強 LLM 方法常把 KG 當成事實集合，未充分使用圖中的關係結構；直接生成可執行邏輯查詢也可能得到無效查詢或不忠實推理。RoG 研究在 KGQA 中如何以圖關係路徑限制檢索與回答，並產生較可追溯的推理依據。[pp. 1–3, §1–3]

## 核心方法與技術架構 (Methodology & Architecture)
RoG 採 **planning–retrieval–reasoning**：規劃器產生 top-K relation paths；執行這些關係序列，從 KG 取回與問題實體連接的有效推理路徑；推理器將問題與取回路徑輸入 LLM 產生答案。規劃器及推理器可分別訓練，論文也測試把規劃模組接到其他 LLM。訓練樣本的規劃監督由問題與答案實體間的最短路徑構造。[pp. 4–6, §4]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, p. 7：** WebQSP / CWQ 上，RoG 的 Hits@1 為 85.7 / 62.6，F1 為 70.8 / 56.2。該表混合不同架構和設定的既有基線；作者報告使用 LLaMA2-Chat-7B，並在 WebQSP、CWQ 訓練資料及 Freebase 上 instruction-finetune 3 epochs，因此結果不能解讀為純零樣本或與任意 API LLM 同條件比較。
- **Table 2, p. 8：** 拿掉規劃模組後，WebQSP / CWQ F1 從 70.81 / 56.17 降至 49.69 / 33.76；拿掉推理模組時 precision 明顯下降，支持兩個模組在此實驗的作用。
- **資料及資源：** WebQSP、CWQ 使用 Freebase；補充的 MetaQA-3hop 使用 Wiki-Movies KG。附錄 §A.6 記載 RoG 訓練使用 2 張 A100-80G GPU 約 38 小時；推論細節採 top-K relation paths。這是本文訓練資源敘述，不能和未報硬體或不同資料/訓練流程的系統直接作成本比較。[§5.1–5.2, pp. 6–8；Appendix A.6, p. 19]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** relation path 是可檢查的結構化計畫；消融顯示規劃和推理兩階段均對本文 KGQA 設定有貢獻。規劃模組可接到其他 LLM，降低對單一生成模型的綁定。
- **限制與代價：** 主要 RoG 模型需要監督式微調及相當 GPU 訓練時間；路徑品質受 topic entity、KG 覆蓋及 relation-path 訓練監督影響。資料集答案實體若不在圖中，圖路徑無法支持答案。主要評估集中於 Freebase KGQA，不能直接外推至自由文本 GraphRAG 或文件級摘要。
- **比較邊界：** 主表中的競品指標並非全數由作者以同一硬體重跑；引用數字應保留原始表格設定及 baseline provenance。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將 RoG 歸入 **D05 Query Understanding & Retrieval**，並以 D09 標示答案必須依檢索路徑 grounded reasoning；paradigm tags 為 `graph_rag`、`multi_hop_rag`。此 taxonomy mapping 是本庫整理方式。相較 ToG 的推理時互動 beam search，RoG 的關鍵對照是以 relation-path 規劃及訓練監督換取結構化檢索流程。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式全文：[ICLR 2024 proceedings PDF](https://proceedings.iclr.cc/paper_files/paper/2024/file/3e2aeb66481dd63a32421bf032b70384-Paper-Conference.pdf)；[arXiv:2310.01061](https://arxiv.org/abs/2310.01061)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2024-05) Reasoning on Graphs - Faithful and Interpretable Large Language Model Reasoning.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph|ToG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Simple is Effective - The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation|SubgraphRAG]]。
