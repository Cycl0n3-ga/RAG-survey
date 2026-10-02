---
paper_id: "Liang2025_KAG"
title: "KAG: Boosting LLMs in Professional Domains via Knowledge Augmented Generation"
authors: ["Lei Liang", "Zhongpu Bo", "Zhengke Gui", "Zhongshu Zhu", "Ling Zhong", "Peilong Zhao", "Mengshu Sun", "Zhiqiang Zhang", "Jun Zhou", "Wenguang Chen", "Wen Zhang", "Huajun Chen"]
year: 2024
publication_year: 2025
venue: "Companion Proceedings of the ACM on Web Conference 2025"
doi: "10.1145/3701716.3715240"
arxiv: "2409.13731"
url: "https://doi.org/10.1145/3701716.3715240"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation.pdf"
tags: ["paper", "professional-domain-qa", "logical-form-reasoning"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D12"
primary_domain: "D12"
secondary_domains: ["D04", "D05"]
paradigm_tags: ["graph_rag", "hybrid_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["logical-form-guided-retrieval", "kg-chunk-mutual-indexing", "domain-knowledge-alignment"]
benchmark_ids: ["HotpotQA", "2WikiMultiHopQA", "MuSiQue"]
dataset_ids: ["HotpotQA", "2WikiMultiHopQA", "MuSiQue", "CMedQA", "BioASQ"]
metrics: ["Exact Match", "F1", "Recall@2", "Recall@5", "ROUGE-L", "BLEU"]
preprint_authors: ["Lei Liang", "Mengshu Sun", "Zhengke Gui", "Zhongshu Zhu", "Zhouyu Jiang", "Ling Zhong", "Yuan Qu", "Peilong Zhao", "Zhongpu Bo", "Jin Yang", "Huaidong Xiong", "Lin Yuan", "Jun Xu", "Zaoyang Wang", "Zhiqiang Zhang", "Wen Zhang", "Huajun Chen", "Wenguang Chen", "Jun Zhou"]
source_version: arXiv:2409.13731v3
verified_version: arXiv:2409.13731v3
pdf_pages: 33
pdf_sha256: b18ac8a05ba486b85c4306a49b726e45d5ba24835b305699d79440876f315b72
---

# KAG: Boosting LLMs in Professional Domains via Knowledge Augmented Generation

> **版本與閱讀範圍：** 正式出版記錄為 WWW 2025 Companion，頁 334–343，DOI 10.1145/3701716.3715240；本次 ACM publisher PDF 端點回 403，故未取得正式版全文。本地全文為 arXiv:2409.13731 v3（2024-09-27，19 位作者），已讀全文；正式版作者名單（12 位）依 DOI metadata，與預印本作者及順序不同。以下方法與實驗明確指向 arXiv v3，不宣稱已驗證正式版正文相同。

## 一話摘要 (TL;DR)
KAG 將知識圖與原文 chunks 互相索引，並以 logical-form-guided hybrid solver 執行檢索、排序、計算、推導與反思，支援專業領域及多跳 QA。

## 研究背景與問題定義 (Problem Statement)
作者指出向量相似度與推理所需知識相關性可能不一致；單靠向量檢索也可能忽略數值、時間、規則等邏輯條件。本文提出面向專業知識服務的 KG＋文本 hybrid framework，並評估多跳 QA 與 Ant Group 的政務、健康問答案例。[arXiv v3 §§1–2, pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
KAG 的設計包括 LLM-friendly knowledge representation、KG 與原始 chunks 的 mutual indexing、logical-form-guided hybrid reasoning、knowledge alignment，以及模型能力增強。檢索端將圖上的 entity/relation 與文本 chunk 建交叉索引，支援從任一側定位證據；logical form solver 將複合問題轉為可執行步驟，使用 retrieval、sort、math、deduce 等 operator，並可在答案不足時反思和補問題。預印本文也介紹 OneGen 作檢索生成聯合模型，但該元件與 KAG 的主 solver 評估應分清。[§§2.2–2.5, pp. 5–12]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 8, 本地 arXiv v3 PDF p. 18：** 多跳 QA 以 DeepSeek-V2 API 比較，KAG `LFSH_ref3` 在 HotpotQA／2WikiMultiHopQA／MuSiQue 的 EM 為 62.5／67.8／36.7，F1 為 76.2／76.2／48.7；同 backbone 的 IRCoT+HippoRAG F1 為 63.7／57.1／36.5。依表中列值計算，KAG 相對該 baseline 的 F1 增幅約 19.6%／33.5%／33.4%（本筆記按表格自行計算）。同表另含 ChatGPT-3.5 組別，不應跨 backbone 混作控制比較。
- **Table 11, 本地 arXiv v3 PDF p. 20：** `LFSH_ref3` 的 Recall@5 為 HotpotQA 88.8、2Wiki 91.9、MuSiQue 65.6；作者註明部分 LFS 路徑可用 KG 推理而不檢索支持 chunks，相關 recall 行因此不可直接比較。
- **專業領域案例：** Table 6, 本地 arXiv v3 PDF p. 16 的 CMedQA／BioASQ 表列 Rouge-L、BLEU；例如 KAG_Llama2 相對 Llama2 的四項分數為 15.44／3.46／24.21／7.79 對 14.02／2.86／23.47／7.11。不同資料和指標分開報告，不與 QA F1 合併排名。
- **條件與資源：** 主多跳端到端比較採 DeepSeek-V2 API、三個資料集；各 1,000 個 test problems，最多 3 輪 reflection，20 個並行 task。論文另有 GPT-3.5 結果及 OneGen 實驗；未提供可比的整體 GPU／API 成本帳。[§3–4；Tables 6, 8, 11；Figure 8]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** operator 讓數學、排序與邏輯操作明確化；mutual indexing 將結構化圖知識與原文依據連起來，便於多跳問題沿兩種表示取證。預印本以消融、retrieval recall 和端到端結果分開檢驗組件。
- **限制與代價：** 多個索引、抽取／對齊與可執行 solver 提高建置與維護複雜度；多輪反思延長推論流程。部分資料由論文系統整理，專業 QA 案例未以同樣公開基準量化，且文內方法效果依模型/API、operator 實作及 reflection 次數而異。
- **比較邊界：** 上列實驗數據來自 arXiv v3，正式 WWW Companion 正文未取得，不能把預印本數據稱為已核的出版版結果；跨 ChatGPT-3.5 與 DeepSeek-V2 的列也不可視為同條件比較。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸入 **D12 RAG Orchestration & Action Control**：主要研究對象是將問題變為 operator 序列並控制 retrieval／reasoning／reflection 行動；D04 表示圖–chunk 表示及互索引，D05 表示 hybrid retrieval。雖然 KAG 同時是一套 GraphRAG，主要分類依 lifecycle 問題，不由名稱決定。它適合與 StructGPT 比較可執行介面，以及與 HybGRAG 比較圖／文本 retrieval 的選擇機制。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 正式書目：[ACM DOI 10.1145/3701716.3715240](https://doi.org/10.1145/3701716.3715240)；[arXiv:2409.13731 v3 全文](https://arxiv.org/abs/2409.13731)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(WWW Companion 2025-04) KAG - Boosting LLMs in Professional Domains via Knowledge Augmented Generation.pdf|開啟本地 arXiv v3 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2023-12) StructGPT - A General Framework for Large Language Model to Reason over Structured Data|StructGPT]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases|HybGRAG]]。
