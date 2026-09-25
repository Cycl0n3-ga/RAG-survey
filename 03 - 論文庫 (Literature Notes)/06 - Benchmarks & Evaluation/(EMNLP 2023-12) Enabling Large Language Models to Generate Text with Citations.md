---
paper_id: "Gao2023_ALCE"
title: "Enabling Large Language Models to Generate Text with Citations"
authors:
  - "Tianyu Gao"
  - "Howard Yen"
  - "Jiatong Yu"
  - "Danqi Chen"
year: 2023
publication_year: 2023
venue: "EMNLP 2023"
doi: "10.18653/v1/2023.emnlp-main.398"
arxiv: "2305.14627"
url: "https://arxiv.org/abs/2305.14627"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(EMNLP 2023-12) Enabling Large Language Models to Generate Text with Citations.pdf"
domains: []
- "[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]"
  - "[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]"
  - "[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]"
tags:
  - paper
  - benchmark
  - citation
  - factual-correctness
  - natural-language-inference
verification_status: "verified"
last_verified: 2026-09-25
artifact_type: "benchmark_paper"
benchmark_ids:
  - "ALCE"
  - "ASQA"
  - "QAMPARI"
  - "ELI5"
metrics:
  - "Citation Recall"
  - "Citation Precision"
  - "STR-EM"
  - "QA-F1"
  - "ROUGE-L"
taxonomy_version: "v2"
taxonomy_home: "D09"
primary_domain: "D09"
secondary_domains:
  - "D13"
paradigm_tags:
  - "citation_aware_rag"
adjacent_interfaces: []

---

# Enabling Large Language Models to Generate Text with Citations (ALCE)

## 一話摘要 (TL;DR)
普林斯頓大學提出的 ALCE（Automatic LLMs' Citation Evaluation）是首個端到端可重現的自動化引文評測基準，透過自然語言推理（NLI）嚴格定義了「引文召回率（Citation Recall：生成宣稱是否被引文完全蘊含）」與「引文精準度（Citation Precision：所引段落是否均為必要支撐）」，揭示即使是最先進的 GPT-4 與 ChatGPT，在長篇生成中仍有大量引文存在虛假掛載與無效引用。

---

## 研究背景與問題定義 (Problem Statement)
現有在長篇文本中增強可驗證性的研究（如 WebGPT、GopherCite）存在重大科研復現瓶頸：
1. **依賴商用搜尋引擎與動態網頁**：先前的系統將模型與線上 Bing/Google 綁定，網頁內容隨時間變動，無法提供標準化、凍結的固定評測環境。
2. **人工評估成本高且不可擴展**：仰賴人工標註逐條判斷引用質量，無法用於日常研究的敏捷迭代與大規模消融實驗。
3. **缺乏引文質量的數學化界定**：文獻中對「引用好不好」缺乏公認的形式化指標，往往將「引用了某篇文檔」與「該文檔確實能推導出該語句」混為一談。

---

## 核心方法與技術架構 (Methodology & Architecture)

ALCE 構建了**標準化三維任務語料庫**與**基於自然語言推理（NLI）的自動引用打分協議**：
1. **三大多樣化資料集構建（Table 1, Page 2）**：
   - **ASQA**（歧義事實問題，語料庫 Wikipedia 21M）：測試模型綜合多個分歧事實並精準標註引用的能力；
   - **QAMPARI**（多實體清單查詢，語料庫 Wikipedia 21M）：測試清單式回答的廣泛引用覆蓋；
   - **ELI5**（解釋性開放長問答，語料庫 Sphere 899M）：測試宏觀因果解釋的深度引用。
2. **引文品質形式化定義（Citation Quality Metrics）**：
   - 設回答文字被劃分為多個語意單元（Segments）$s_1, s_2, \dots, s_n$，每個單元附帶引用的文檔集合 $C(s_i)$：
   - **引文召回率（Citation Recall）**：
     - 若 $C(s_i)$ 中的文檔拼接後能夠**完全蘊含（Entail）** $s_i$，則判定該語意單元受支撐；
     - $\text{Citation Recall} = \frac{\sum_{i=1}^n \mathbb{I}(\text{Entail}(C(s_i), s_i))}{n}$。
   - **引文精準度（Citation Precision）**：
     - 檢查 $C(s_i)$ 中的每一個被引用文檔 $c \in C(s_i)$，若移除 $c$ 後不再構成充分蘊含，或 $c$ 本身提供了不可或缺的事實支撐，則視為有效引用；
     - 懲罰「胡亂掛載多篇不相關文檔」的取巧行為（Shortcut Gaming）。
3. **回答正確性指標（Answer Correctness）**：
   - 結合短事實 Exact Match（STR-EM）、QA-F1 與 ROUGE-L，確保模型在提高引用的同時不犧牲回答實質內容。

```mermaid
flowchart TD
    subgraph input["查詢與檢索篇章"]
        Q["用戶問題 (Query)"] --> RET["標準檢索器 (Dense / Sparse Retriever)"]
        RET --> PASS["Top-k 檢索文檔 [1]..[k]"]
    end

    subgraph generation["引文生成模組"]
        Q --> LLM["生成模型 (LLM with Prompting)"]
        PASS --> LLM
        LLM --> TEXT["生成回答 (帶有標記 [1][2])"]
    end

    subgraph nli_eval["ALCE 自動化 NLI 評測管線"]
        TEXT --> SPLIT["拆分為句子/語意片段 s_i"]
        SPLIT --> NLI{"TRUE / AUTO NLI 模型"}
        PASS -.->|對應引文 C(s_i)| NLI
        NLI --> REC["Citation Recall: 是否完全被蘊含？"]
        NLI --> PREC["Citation Precision: 是否每個引用皆必要？"]
    end

    subgraph output_metrics["綜合評估指標"]
        REC --> R_SCORE["Citation Recall (%)"]
        PREC --> P_SCORE["Citation Precision (%)"]
        TEXT --> CORR["Answer Correctness (STR-EM / QA-F1)"]
    end
```

### 圖中節點對照
- `PASS`：凍結的標準候選文本庫篇章。
- `SPLIT`：語意單元分詞模組。
- `NLI`：預訓練自然語言推理判別器（如 TRUE 模型）。
- `REC` / `PREC`：形式化引文召回與精準度評分。

---

## 主要實驗結果與證據 (Empirical Results & Evidence)

論文評測了 ChatGPT (gpt-3.5-turbo)、GPT-4、LLaMA-2-Chat 等多種主流模型與 Prompting 策略（VANILLA, RERANK, SUMMARY, SNIPPET）。

### ASQA 基準評測結果 (Table 4, Page 6)
- **ChatGPT (VANILLA, 5-psg)**：
  - 正確性（STR-EM Rec.）：**40.4%**；
  - 引文召回率（Citation Recall）：**73.6%**；
  - 引文精準度（Citation Precision）：**72.5%**。
- **ChatGPT w/ RERANK (檢索重排)**：
  - 正確性：40.2%；
  - 引文召回率提升至 **84.8%**（提升 **+11.2%**）；
  - 引文精準度提升至 **81.6%**。
- **GPT-4 (5-psg vs 20-psg)**：
  - 5-psg：正確性 41.3%，Recall 68.5%，Precision 75.6%；
  - 20-psg：正確性 44.4%，Recall **73.0%**，Precision **76.5%**。
- **開源模型 LLaMA-2-Chat-70B (5-psg)**：
  - 正確性 41.5%，Citation Recall 62.9%，Precision 61.3%（顯著落後於 GPT-4，存在較多虛假引用掛載）。
- **ELI5 長篇解釋基準挑戰**：
  - 即使是最佳模型，在 ELI5 上的引文召回率僅約 50% 左右，說明在需要深度綜合與推理的長篇開放論述中，模型仍習慣性依賴內部先驗偏好進行未受支持的自由發揮。

---

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)

### 優勢
1. **完全開源可復現**：提供端到端自動評測代碼與凍結語料，終結了依賴即時 Web 搜尋導致不可對比的歷史。
2. **直擊引文虛標痛點**：首次精準區分了「文檔是否覆蓋了宣稱（Recall）」與「引用是否多餘或不相干（Precision）」，杜絕了模型盲目在每句話後堆砌大量無關引用的捷徑攻擊。

### 限制與 Trade-offs
1. **依賴 NLI 模型判斷**：作為評委的 NLI 模型（如 TRUE/T5-XXL）本身存在一定的判斷偏差，在涉及細微數字、否定與條件限定詞時可能出現誤判。
2. **粒度劃分難題**：以 Sentence 還是 Sub-sentence 作為評估單元對最終分數有直接影響。

---

## 對本專案研究領域的實際意義 (Implications for Research Domains)
1. **對 D09 (Grounded Generation & Long-form Synthesis) 的核心標準意義**：為長篇報告系統（如 STORM、EviReport）提供了權威可量化的自動引文驗證指標。
2. **對 D09/D13 (Attribution & Evaluation) 的直接落地**：ALCE 的 Citation Recall/Precision 計算邏輯可直接作為本專案 Evidence Ledger 治理管線中的自動審核算子。

---

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 原始論文 PDF：[[Papers/06 - Benchmarks & Evaluation/(EMNLP 2023-12) Enabling Large Language Models to Generate Text with Citations.pdf|開啟本地 PDF]]
- arXiv 永久連結：[arXiv:2305.14627](https://arxiv.org/abs/2305.14627)
- 關聯專題領域：[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]、[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]、[[02 - 研究領域專題 (Research Domains)/Canonical RAG Domains/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
