---
paper_id: "Xiang2026_WhenToUseGraphsInRAG"
title: "When to use Graphs in RAG: A Comprehensive Analysis for Graph Retrieval-Augmented Generation"
authors: ["Zhishang Xiang", "Chuanjie Wu", "Qinggang Zhang", "Shengyuan Chen", "Zijin Hong", "Xiao Huang", "Jinsong Su"]
year: 2025
publication_year: 2026
venue: "ICLR 2026"
doi: null
arxiv: "2506.05690"
url: "https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(ICLR 2026-04) When to use Graphs in RAG - A Comprehensive Analysis for Graph Retrieval-Augmented Generation.pdf"
tags: ["paper", "GraphRAG-Bench", "comparative-evaluation"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "benchmark_paper"
taxonomy_version: "v2"
taxonomy_home: "D13"
primary_domain: "D13"
secondary_domains: ["D04", "D05", "D09"]
paradigm_tags: ["graph_rag"]
adjacent_interfaces: []
research_questions: ["graph_rag_task_fit", "reasoning_complexity", "stage_wise_evaluation", "retrieval_cost"]
benchmark_ids: ["GraphRAG-Bench"]
dataset_ids: ["GraphRAG-Bench-Novel", "GraphRAG-Bench-Medical"]
metrics: ["Accuracy", "ROUGE-L", "Context Relevance", "Evidence Recall", "Faithfulness", "Evidence Coverage", "Token Cost"]
---

# When to use Graphs in RAG: A Comprehensive Analysis for Graph Retrieval-Augmented Generation

## 一話摘要 (TL;DR)
本文提出 GraphRAG-Bench，按檢索難度與推理複雜度評估 GraphRAG，顯示圖方法的效益依任務而變，並伴隨建圖與 prompt token 成本。

## 研究背景與問題定義 (Problem Statement)
既有評測常以短 passage 和有限 hop 數表示多跳任務，未必測到跨概念整合、階層化知識推理及長篇綜述。作者要測量圖結構何時能改善 RAG，並分辨失敗來自圖索引、檢索或生成，而非只看單一端到端分數。[§1–3, pp. 1–6]

## 核心方法與技術架構 (Methodology & Architecture)
GraphRAG-Bench 用兩種不同知識型態的語料建立 Novel 與 Medical 評測集，設計 Fact Retrieval、Complex Reasoning、Contextual Summarize、Creative Generation 四類任務；依知識廣度與推理深度控制難度。評估分為生成品質、Context Relevance、Evidence Recall、圖結構統計及 token 成本。比較包含 Vanilla RAG、Microsoft GraphRAG、HippoRAG/2、LightRAG、FastGraphRAG、RAPTOR、Lazy-GraphRAG 等方法。[§3, pp. 4–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 3, p. 7：** GPT-4o-mini 生成評估呈現任務差異。在 Novel Complex Reasoning，HippoRAG2 Accuracy / ROUGE-L 為 53.38 / 33.42，reranked Basic RAG 為 42.93 / 15.39；但在 Novel Fact Retrieval，reranked Basic RAG 為 60.92 / 36.08，不能概括成 GraphRAG 一律較佳。
- **Table 4, p. 8：** Novel Complex Reasoning 的 Evidence Recall / Context Relevance，HippoRAG 為 87.91 / 58.75，HippoRAG2 為 69.77 / 85.75；反映召回完整度和相關性不同，應分開讀取。
- **Tables 6–7, p. 9：** 平均輸入 token 數在 Novel 資料集，Vanilla RAG 為 879、Microsoft GraphRAG global 為 331,375、LightRAG 為 100,832、HippoRAG2 為 1,008；各方法 prompt 組成不同，數字是本文實作下的成本，不代表所有配置。
- **設定：** Table 3–4 使用 GPT-4o-mini；Novel 語料為小說、Medical 語料為 NCCN 臨床指引。全文未在主要設定中報出硬體型號。結果限於該 benchmark、所選模型和本文 pipeline。[§4, Tables 3–7, pp. 7–9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 不只看 QA，亦分開量 retrieval、graph structure、generation 與 token 成本；Novel 與 Medical 語料可對照隱含敘事依賴和顯式專業階層。
- **限制與代價：** 兩類自建語料不能代表所有產業或自然查詢分布；多個方法由作者在統一框架中實作，仍受實作與 prompt 選擇影響；圖建置耗用時間和 tokens。表中缺值或因超時未完成者不可視為零分。
- **比較邊界：** 各項分數只適合在本文同一 dataset、同一 task 和列明配置內比較；跨任務比較或與其他論文數字不構成受控比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
歸入 **D13 Evaluation & Failure Attribution**，次領域 D04/D05/D09，因主要貢獻是整體評測與效益條件分析。它可作比較 GraphRAG 與 LightRAG 的共同基準來源；具體方法效能仍須回到各方法原始論文核對，不用此文替代 primary papers。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ICLR 2026 官方論文頁](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html)；[arXiv:2506.05690（2025 預印、全文）](https://arxiv.org/abs/2506.05690)。正式出版年份為 2026，預印初次上傳為 2025。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(ICLR 2026-04) When to use Graphs in RAG - A Comprehensive Analysis for Graph Retrieval-Augmented Generation.pdf|開啟 ICLR 正式版 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-08) Graph Retrieval-Augmented Generation - A Survey|Graph Retrieval-Augmented Generation: A Survey]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-10) LightRAG - Simple and Fast Retrieval-Augmented Generation|LightRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICML 2025-07) From RAG to Memory - Non-Parametric Continual Learning for Large Language Models|HippoRAG 2]]。
