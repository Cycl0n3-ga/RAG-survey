---
paper_id: "Tan2025_HydraRAG"
title: "HydraRAG: Structured Cross-Source Enhanced Large Language Model Reasoning"
authors:
  - "Xingyu Tan"
  - "Xiaoyang Wang"
  - "Qing Liu"
  - "Xiwei Xu"
  - "Xin Yuan"
  - "Liming Zhu"
  - "Wenjie Zhang"
year: 2025
publication_year: 2025
venue: "EMNLP 2025"
doi: "10.18653/v1/2025.emnlp-main.730"
arxiv: "2505.17464"
url: "https://aclanthology.org/2025.emnlp-main.730/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) HydraRAG - Structured Cross-Source Enhanced Large Language Model Reasoning.pdf"
tags:
  - paper
  - cross-source-verification
  - graph-text-rag
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains:
  - "D08"
  - "D12"
paradigm_tags:
  - "graph_rag"
  - "hybrid_rag"
  - "agentic_rag"
adjacent_interfaces: []
research_questions:
  - "hybrid_graph_text_retrieval"
  - "cross_source_verification"
  - "multi_hop_retrieval"
  - "agentic_retrieval_control"
benchmark_ids:
  - "ComplexWebQuestions"
  - "WebQSP"
  - "AdvHotpotQA"
  - "QALD10-en"
  - "SimpleQA"
  - "ZeroShot RE"
  - "WebQuestions"
dataset_ids:
  - "Freebase"
  - "Wikipedia"
  - "Wikidata"
metrics:
  - "Hits@1 / exact-match accuracy"
  - "average total time"
  - "API calls per question"
source_version: arXiv:2505.17464v4
verified_version: arXiv:2505.17464v4
pdf_pages: 29
pdf_sha256: 9d85f333bc74d07887f87c249c23eaf4055b3ec6182a5c062ffba3337b5bdc20
---

# HydraRAG: Structured Cross-Source Enhanced Large Language Model Reasoning

> **版本與閱讀範圍：** arXiv:2505.17464 v4（最後修訂 2025-09-19，本地 PDF 29 頁）全文已讀；ACL Anthology 正式書目與 abstract 已核。正式論文刊於 EMNLP 2025，頁 14431–14459，DOI `10.18653/v1/2025.emnlp-main.730`；本地 PDF 為 arXiv v4，未逐段比對 proceedings PDF 與預印本版本。

## 一話摘要 (TL;DR)
HydraRAG 以 agent-driven exploration 聯合搜尋 KG、Wikipedia 與 web documents，再用來源可靠度、跨源互證與 entity-path alignment 對 evidence paths 篩選和精煉，支援多跳、多實體問答。

## 研究背景與問題定義 (Problem Statement)
作者指出，只用文字向量檢索不易串接分散於多文件的 entity facts；只靠知識圖譜也受 coverage／更新範圍限制；直接拼接多來源 evidence 則把 source reliability 與 cross-source consistency 留給 LLM 自行判斷。HydraRAG 探討如何在 inference time 協調 text 和 KG retrieval、擴展推理路徑並對來源作多面向驗證。[§1, arXiv PDF pp. 1–2；§3, pp. 3–4]

## 核心方法與技術架構 (Methodology & Architecture)
HydraRAG 為 training-free framework。系統先分析問題與 topic entities，再由 agent 逐輪探索圖與文字來源；對取得的候選 paths 使用多階段 pruning，評估 semantic relevance、source trustworthiness、cross-source corroboration 與 entity/path alignment；path refinement 將保留資訊整理成較聚焦的 evidence，最後由 LLM 根據 evidence paths 推理和回答，若尚無可用路徑則可繼續探索。[§4, Figures 2–3, arXiv PDF pp. 4–7]

方法內含 source-specific graph／text retrieval 和 LLM controller；這些是本文系統設計，不應把它們拆寫成四個獨立已驗證方法。論文在 appendix 描述背景知識來源包括 Freebase、Wikipedia、Wikidata；retrieval 用 SentenceBERT，generation 以 GPT-3.5-Turbo 為主，亦測試多個不同 backbone。[Appendix C, arXiv PDF p. 22]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv PDF p. 8：** 在 GPT-3.5-Turbo 設定下，HydraRAG 對 CWQ、WebQSP、AdvHotpotQA、QALD10-en、SimpleQA、ZeroShot RE、WebQuestions 的 Hits@1／exact-match accuracy 依序為 81.2、96.1、58.9、84.2、88.8、97.7、88.3。各資料集任務不同，不應把分數跨資料集直接排序；Table 1 的 ToG-2 LLM 欄位未填，直接方法比較需保留該設定不確定性。
- **Table 2, arXiv PDF p. 9：** 四資料集、多 backbone 的 IO vs HydraRAG comparison；作者報 Llama-3.1-8B 的平均相對提升 132%，ZeroShot RE 最高提升 185%。這是表中指定 accuracy 與同資料／backbone 配對的結果，不代表在其他任務或未測模型上可達同樣增幅。
- **Table 9, arXiv PDF p. 21：** AdvHotpotQA 上 HydraRAG 平均每題 43.0 秒、8.7 次 API calls、accuracy 60.7%；ToG-2 為 27.3 秒、5.4 次 calls、42.9%；ToG 為 69.3 秒、16.3 次 calls、26.3%。此為論文報告的特定 benchmark／實作／模型呼叫條件，顯示精度、延遲及 API 呼叫量的取捨；不能推成一般部署成本結論。
- **評測協議：** Appendix C 說明七個 KBQA benchmark 使用既有工作所報 sampled test splits，背景 KG/text sources 為 full Freebase、Wikipedia、Wikidata；主指標採 Hits@1 / exact match，不報 recall/F1。本文未建立跨硬體統一 GPU 成本比較。[Appendix C, arXiv PDF p. 22]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- 將 KG 路徑與 document/web evidence 納入共同的 exploration / verification process，並把 source trust 和 corroboration 寫入篩選步驟；Table 9 同時顯示相較較快的 ToG-2，HydraRAG 使用更多時間與 API calls。[Appendix B.5, arXiv PDF p. 21]
- 作者的 Limitations 明確指出目前聚焦於 character-based knowledge sources，尚未納入 image/video 等外部模態。[§8, arXiv PDF p. 10]
- 結果依賴特定多來源語料、既有 benchmark test splits、LLM / search tools 與 prompt 設定；跨源互證打分不等同一般 provenance governance、權威性審查或完整 evidence sufficiency 控制。對 ToG-2 的論文平均增幅宣稱應與其資料、prompt 和模型條件一併呈現。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
建議 D05 primary，因主要問題是 query-time hybrid graph/text retrieval 與路徑擴展；D08 secondary 對應 source reliability 與跨來源 corroboration；D12 secondary 對應 agent-driven exploration 和停止／再探索流程。這是 repo 的 operational taxonomy，不是作者原有分類。對 graph-heavy RAG 比較可與 ToG-2、HybGRAG、GeAR 並列，但需控制來源範圍、LLM、candidate/step budget、prompt、test split 和 API cost；本文是較接近 text+KG+web 多源設定的系統性案例。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式來源：[ACL Anthology 正式記錄與 PDF](https://aclanthology.org/2025.emnlp-main.730/)；預印本版本記錄：[arXiv:2505.17464](https://arxiv.org/abs/2505.17464)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2025-11) HydraRAG - Structured Cross-Source Enhanced Large Language Model Reasoning.pdf|開啟本地 PDF 檔案]]（arXiv v4；29 頁）。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases|HybGRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation|GeAR]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2025-05) Think-on-Graph 2.0 - Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation|ToG-2]]。
