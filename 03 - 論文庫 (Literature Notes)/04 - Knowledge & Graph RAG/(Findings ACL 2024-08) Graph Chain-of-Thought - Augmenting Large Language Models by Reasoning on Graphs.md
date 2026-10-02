---
paper_id: "Jin2024_GraphCoT_GRBench"
title: "Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs"
authors:
  - "Bowen Jin"
  - "Chulin Xie"
  - "Jiawei Zhang"
  - "Kashob Kumar Roy"
  - "Yu Zhang"
  - "Zheng Li"
  - "Ruirui Li"
  - "Xianfeng Tang"
  - "Suhang Wang"
  - "Yu Meng"
  - "Jiawei Han"
year: 2024
publication_year: 2024
venue: "Findings of the Association for Computational Linguistics: ACL 2024"
doi: "10.18653/v1/2024.findings-acl.11"
arxiv: "2404.07103"
url: "https://aclanthology.org/2024.findings-acl.11/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) Graph Chain-of-Thought - Augmenting Large Language Models by Reasoning on Graphs.pdf"
tags:
  - paper
  - graph-reasoning
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D12"
  - "D13"
paradigm_tags:
  - "graph_rag"
  - "multi_hop_rag"
adjacent_interfaces: []
research_questions:
  - "text_attributed_graph_retrieval"
  - "iterative_graph_reasoning"
  - "graph_reasoning_evaluation"
benchmark_ids:
  - "GRBench"
dataset_ids:
  - "GRBench"
metrics:
  - "ROUGE-L"
  - "GPT-4 judged accuracy"
source_version: arXiv:2404.07103v3
verified_version: arXiv:2404.07103v3
pdf_pages: 22
pdf_sha256: 8b61c9a5792f456bf8533e47bc1d3bc14cf6ca8ded49ac4905d9d58a4f20ce95
---

# Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs

> **版本與閱讀範圍：** arXiv:2404.07103 首次提交於 2024-04-10，本地保存 arXiv v3（2024-10-03，22 頁）；正式論文刊於 Findings of ACL 2024，頁 163–184，DOI `10.18653/v1/2024.findings-acl.11`。已讀 arXiv v3 全文並核對 ACL 正式書目；尚未逐段比對 arXiv v3 與 proceedings PDF 的差異。下列頁碼同時標明本地 PDF 頁碼。

## 一話摘要 (TL;DR)
Graph-CoT 讓 LLM 以「自然語言推理、呼叫圖操作、執行圖查詢」反覆在 text-attributed graph 上找證據，並以 GRBench 評測跨圖推理。

## 研究背景與問題定義 (Problem Statement)
作者指出，text-attributed graph 的證據不只存在節點文字，也存在節點間連結；只把圖線性化成大段文字會引入無關上下文，擴大多跳問題的輸入長度。論文因此同時提出 Graph-CoT 方法與 GRBench，研究 LLM 如何按問題迭代探索外部圖。[§1, pp. 163–165；arXiv PDF pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
Graph-CoT 每輪由三步組成：LLM reasoning 根據問題與已取得資訊提出下一個子問題；LLM-graph interaction 產生圖操作呼叫；graph execution 在指定圖上執行操作並把結果交回下一輪。直到模型呼叫 Finish，輸出答案。圖以節點文字與關係定義供模型互動，並以示範提示教模型使用操作介面。[§3, Figure 2, pp. 165–167；arXiv PDF pp. 3–5]

GRBench 收錄 10 個真實 text-attributed graphs，涵蓋學術、電商、文學、醫療與法律五個領域，共 1,740 題；題目分單跳、需多跳與歸納推理難度。此 benchmark 同時測試圖檢索／互動及回答品質，並非通用 GraphRAG 評測的完整替代品。[§2, Table 1, pp. 164–165；§7, p. 170；arXiv PDF pp. 2, 9]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, p. 168（arXiv PDF p. 6）：** Graph-CoT 以 GPT-3.5-turbo 作 backbone，在 Academic、E-commerce、Literature、Healthcare、Legal 五領域的 GPT-4 判分依序為 `33.48, 44.50, 46.25, 28.89, 28.33`；同 backbone 的 Graph RAG baseline 依序為 `26.98, 28.00, 24.17, 14.07, 22.22`。分數是該 GRBench 設定中的 Rouge-L／GPT4score 評估結果，不能直接外推到其他圖、問題分布或 RAG 系統。
- **Table 3, p. 169（arXiv PDF p. 7）：** Graph-CoT 在抽樣子集上以 LLaMA-2-13B-chat、Mixtral-8x7B、GPT-3.5-turbo、GPT-4 作 backbone 時，GPT4score 分別為 `16.04, 36.46, 36.63, 46.28`；樣本是一題型一題，非全 GRBench 結果。
- **評估設定：** 主結果以 GPT-3.5-turbo-16k、temperature 0；基線檢索器用 all-mpnet-base-v2 並以 FAISS 建索引；實驗在 NVIDIA GeForce RTX A6000 上執行。生成式評分由 GPT-4 判斷答案是否正確；作者另報 ROUGE-L。[§5.1, p. 168；arXiv PDF p. 6]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 方法逐步呼叫圖操作，避免一次塞入大型鄰居子圖；Table 4 顯示 Graph-CoT 的 GPT4score 為 36.29，高於單節點檢索 16.63、1-hop ego graph 23.09、2-hop ego graph 22.12 的平均分。[§5.4, Table 4, p. 169；arXiv PDF p. 7]
- 作者報告示範提示對方法很重要：zero-shot Graph-CoT 幾乎無法完成任務；跨領域示範通常仍可工作，但困難與歸納題表現下降。錯誤案例包括把問題詞面映射到不存在的鄰居類型，以及誤解圖結構、呼叫錯誤操作。[§5.3–5.6, pp. 168–170；arXiv PDF pp. 6–8]
- 論文指出 GRBench 的題型多為人工設計，問題多樣性與難度仍可改善；Graph-CoT 的主 backbone 使用不可微調或微調成本高的 API 模型，且複雜圖推理仍有明顯失敗空間。[§7–8, pp. 170–171；arXiv PDF p. 9]
- 以上比較限於論文中的圖、圖操作、提示與模型設定；沒有跨硬體延遲或成本評測，不能據此推定互動式圖查詢較便宜。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 建議以 D05 作主域，因核心問題是 query-time graph retrieval／evidence exploration；D12 表示模型控制操作與停止行為，D13 表示本文同時提出 GRBench。這是 repo taxonomy mapping，不是作者 taxonomy。它可與 KG traversal（ToG、RoG）及 text-attributed graph retrieval（G-Retriever）比較；比較時需區分知識圖譜與 text-attributed graph 的資料形態。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 正式記錄與 PDF](https://aclanthology.org/2024.findings-acl.11/)；[arXiv:2404.07103](https://arxiv.org/abs/2404.07103)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(Findings ACL 2024-08) Graph Chain-of-Thought - Augmenting Large Language Models by Reasoning on Graphs.pdf|開啟本地 PDF 檔案]]（arXiv v3）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(NeurIPS 2024-12) G-Retriever - Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering|G-Retriever]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph|Think-on-Graph]]。
