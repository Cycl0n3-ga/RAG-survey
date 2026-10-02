---
paper_id: "Jiang2023_StructGPT"
title: "StructGPT: A General Framework for Large Language Model to Reason over Structured Data"
authors: ["Jinhao Jiang", "Kun Zhou", "Zican Dong", "Keming Ye", "Wayne Xin Zhao", "Ji-Rong Wen"]
year: 2023
publication_year: 2023
venue: "EMNLP 2023"
doi: "10.18653/v1/2023.emnlp-main.574"
arxiv: "2305.09645"
url: "https://aclanthology.org/2023.emnlp-main.574/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(EMNLP 2023-12) StructGPT - A General Framework for Large Language Model to Reason over Structured Data.pdf"
tags: ["paper", "structured-data-qa", "tool-interface"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D12"
primary_domain: "D12"
secondary_domains: ["D05", "D07"]
paradigm_tags: ["graph_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["iterative-structured-data-access", "llm-interface-invocation", "evidence-guided-structured-reasoning"]
benchmark_ids: ["WebQSP", "MetaQA", "WikiSQL", "WTQ", "TabFact", "Spider"]
dataset_ids: ["WebQSP", "MetaQA", "WikiSQL", "WTQ", "TabFact", "Spider", "Spider-SYN", "Spider-Realistic"]
metrics: ["Hits@1", "Denotation Accuracy", "Accuracy", "Execution Accuracy"]
---

# StructGPT: A General Framework for Large Language Model to Reason over Structured Data

> **版本與閱讀範圍：** 已讀 ACL Anthology 的 EMNLP 2023 正式全文 PDF（15 頁），並核對 arXiv:2305.09645。ACL 書目列第五作者為 Xin Zhao，正式 PDF 首頁以 Wayne Xin Zhao 列名；筆記保留論文 PDF 的較完整作者名，兩者指向同一篇 DOI 記錄。

## 一話摘要 (TL;DR)
StructGPT 以 Iterative Reading-then-Reasoning（IRR）讓 LLM 反覆呼叫 KG、table、database 專用讀取介面，逐步取得結構化證據後回答問題。

## 研究背景與問題定義 (Problem Statement)
LLM 可用自然語言理解部分結構化資料，但直接把整個知識圖、表格或資料庫線性化塞入 prompt，會遇到資料量過大、結構未必能被可靠解析及無關內容干擾。本文研究如何讓模型透過外部介面選取所需資料，再把精力集中於推理，而非自行模仿資料庫查詢或讀完整個資料庫。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
IRR 將一次解題拆為 **invoking → linearization → generation**，並在多輪迭代中重複：LLM 從問題判斷該呼叫哪個資料介面；介面執行實際讀取／篩選並回傳局部結構；系統把回傳結果線性化給 LLM 選下一步或作答。KG 提供 neighbor-relation、triple 等讀取函數；table 提供列／欄選取；DB 提供 schema、table、column 等操作。介面負責精確取數，LLM 負責依資料類型做逐步推理。[§3, pp. 3–5; Figure 1]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **資料與模型：** KGQA 使用 WebQSP、MetaQA 1/2/3-hop；TableQA 使用 WTQ、WikiSQL、TabFact；Text-to-SQL 用 Spider、Spider-SYN、Spider-Realistic。主要評估 Davinci-003 與 June-version ChatGPT，zero-shot 及 few-shot（KGQA 的 WebQSP/MQA 分別 15/32 examples；table/SQL 最多 32）。[§5.1, pp. 5–6]
- **Table 1, 本地 PDF p. 7：** ChatGPT + IRR zero-shot 在 WebQSP／MetaQA 1-hop／2-hop／3-hop 的 Hits@1 為 72.6／94.2／93.9／80.2；基礎 ChatGPT 是 61.2／61.9／31.0／43.2。此處特別反映多跳 MetaQA 的差距，不能把少數資料集外推成一般生成提升。
- **Table 2, 本地 PDF p. 8：** ChatGPT + IRR zero-shot 在 WTQ／WikiSQL／TabFact 為 48.4／54.4／87.1；few-shot 為 52.2／65.6／87.6。原文註明指標是 WTQ、WikiSQL denotation accuracy 與 TabFact accuracy。
- **Table 3, 本地 PDF p. 8：** ChatGPT + IRR zero-shot 在 Spider／Spider-SYN／Spider-Realistic 的 execution accuracy 為 74.8／62.0／70.3，few-shot 為 77.8／64.0／72.0。三張主表中的監督式基線數字取自既有論文，並非作者全部同條件重跑。[§5.4, 本地 PDF pp. 6–8]
- **錯誤分析，Figure 3, p. 9：** WebQSP 的錯誤中 74% 被歸為 relation selection error；Spider 的 reasoning error 約 62%。作者指出不同資料類型的主要失效源不同。[§6, p. 9]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 將外部資料存取交由具體介面執行，減少 prompt 內完整結構資料的負擔；同一 IRR pattern 套用至 KG、table、DB，讓 retrieval/access 和 reasoning 可分開檢查。
- **限制與代價：** 每種資料仍需手工設計工具介面與輸出格式，且循序呼叫可能增加回合／延遲；選錯 relation、工具輸出線性化不佳或格式錯誤仍會失敗。作者自己指出實驗用 instruction-following 能力強的 ChatGPT 與 Davinci-003、範圍限於結構化 QA、生成格式錯誤需按資料集改善 prompt/parser。[§7, pp. 9–10]
- **比較邊界：** Table 1–3 混合原論文監督式結果與作者重跑之 LLM 結果，且模型版本、few-shot 條件不同，不能以單一分數對所有方法作排序。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸入 **D12 RAG Orchestration & Action Control**：核心是 LLM 如何在狀態化步驟中呼叫資料介面並決定下一步；D05 表示針對問題的資料選取，D07 表示取得內容後的利用。它與 KAG 的 logical-form operators 可執行推理、HybGRAG 的文本/關係混合檢索及 critic 形成有用對照。此工作處理結構化資料訪問，並非 GraphRAG corpus 索引方法的同義詞。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式出版頁與全文：[ACL Anthology EMNLP 2023](https://aclanthology.org/2023.emnlp-main.574/)；[DOI 10.18653/v1/2023.emnlp-main.574](https://doi.org/10.18653/v1/2023.emnlp-main.574)；[arXiv:2305.09645](https://arxiv.org/abs/2305.09645)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(EMNLP 2023-12) StructGPT - A General Framework for Large Language Model to Reason over Structured Data.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation|KAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases|HybGRAG]]。
