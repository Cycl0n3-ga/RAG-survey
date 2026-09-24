# Agent 工作守則與專案注意事項 (Project Guidelines for AI Agents)

本專案為 **LLM 超長文件處理、RAG、知識圖譜與長篇生成技術全景知識庫**。
所有在此專案中工作的 AI Agent（包含 Antigravity、Gemini、Claude、Cursor 等）**必須嚴格遵守以下核心工作守則與標準化規範**。

---

## 🎯 核心工作守則 (Core Operational Principles)

### 1. 分支操作原則 (Branch Policy)
- **可以直接在 `master` 分支上操作**。
- 無需強制建立額外的 feature branch，直接在 `master` 分支上進行檔案新增、編輯與維護。

### 2. 作業前置同步 (Pre-Task Sync)
- **每次作業開始前，必須先從 GitHub 遠端同步最新代碼**：
  ```bash
  git fetch origin master && git pull --rebase origin master
  ```
- 確保本機工作目錄與遠端保持完全一致，避免版本分歧或覆蓋他人/其他設備之修改。

### 3. 作業完成自動提交與推送 (Post-Task Commit & Push)
- **每當一個任務或階段性作業完成時，務必執行 `commit` 與 `push`**：
  ```bash
  git add -A
  git commit -m "type(scope): 清楚描述本次更新之實質內容"
  git push origin master
  ```
- 嚴禁作業完成後將未提交的修改留在本地，確保遠端 GitHub 儲存庫始終具備最新的研究筆記與檔案狀態。
- **每次任務或階段性作業完成時，不只要確認有執行 `git push`，在 push 之前務必先完整確認並完成 `git commit`**：
  - 嚴格遵守「檢查狀態 $\to$ 全部暫存 $\to$ 完成提交 $\to$ 遠端推送 $\to$ 驗證乾淨」五步閉環流程：
    ```bash
    # 1. 檢視修改狀態
    git status
    # 2. 將所有新增、修改與刪除之檔案納入暫存
    git add -A
    # 3. 確實執行 commit，嚴禁未 commit 就直接 push
    git commit -m "type(scope): 清楚描述本次更新之實質內容"
    # 4. 推送至遠端 GitHub
    git push origin master
    # 5. 再次確認本地 working tree 乾淨且與遠端同步
    git status
    ```
- **核心鐵律**：
  - **Push 前必須先 Commit**：絕不可在未完成 `git commit` 前就嘗試 `git push`，亦不可誤以為單純 push 就會自動提交暫存區或工作區的修改。
  - **嚴禁遺留本地變更**：任務結束時必須以 `git status` 確認 `nothing to commit, working tree clean`，絕不可將未提交或未推送的修改滯留在本地工作目錄。

### 4. 存疑必問，正確性至上 (Clarify Doubts, Accuracy is Paramount)
- **若對使用者的需求、格式偏好、技術細節或資料來源存在任何懷疑或不確定性，務必主動向使用者詢問釐清，切勿自行腦補或做未經證實的假設**。
- **本專案的核心價值在於學術與工業實踐的高準確度**，正確性永遠高於單純的生成速度。

---

## 📚 可驗證的引用標準 (Verifiable Citation & Reference Standards)

1. **原始來源核對**：
   - 論文的標題、作者列表、發表年份、發表會議/期刊（Venue）、DOI 或 arXiv ID **必須由原始文獻或官方學術索引（arXiv, ACL Anthology, IEEE, ACM, OpenReview 等）直接核對**。
2. **版本區分機制（嚴禁混淆發表年份）**：
   - 必須嚴格區分**預印本（Preprint）**、**正式發表版本（Conference / Journal Published Version）**與**後續擴充修訂版本**。
   - **不得將 arXiv 初次上傳年份直接當成正式會議/期刊發表年份**（例如：某論文 2023 年掛在 arXiv，2024 年被 ICLR 錄取接收，其預印年份為 2023，正式發表年份為 2024）。
3. **實驗數據可溯源性**：
   - 筆記中記錄的所有關鍵實驗數據與基準表現，**應標註對應論文中的具體頁碼、表格編號（Table X）或圖表（Figure Y）**，並註記其評估條件（如模型尺寸、測試長度、Few-shot 設定等）。
4. **誠實原則（嚴禁充數）**：
   - 無法取得論文 PDF 全文時，**不得假裝已閱讀全文**，嚴禁下載與該論文無關的檔案或空檔案充數。若僅能獲取 Abstract，必須在筆記中如實標註為「僅基於摘要整理，全文待查驗」。
5. **查重與版本比對**：
   - 新增論文前，必須先以 **DOI、arXiv ID 或正式學術識別碼** 進行查重。
   - 特別針對預印本、會議論文與後續擴充的期刊版本，**絕不能只憑標題或作者相似就認定內容完全相同**，必須核查章節、定理證明與實驗數據之差異。

---

## 📝 論文筆記標準化 (Literature Note Standardization)

新建立與維護的論文筆記**必須遵循統一的 YAML Frontmatter 及 Markdown 正文結構**。

### 1. YAML Frontmatter 規範
Frontmatter 必須使用固定欄位名稱與一致的資料型別。不得因為新增欄位而任意刪除舊筆記中的既有 metadata。

```yaml
---
paper_id: "Vaswani2017_Attention"                       # 格式：[第一作者姓氏][年份]_[簡短識別名稱]
title: "Attention Is All You Need"                     # 論文完整正式標題 (字串)
authors:                                               # 作者完整陣列 (List of strings)
  - "Ashish Vaswani"
  - "Noam Shazeer"
  - "Niki Parmar"
year: 2017                                             # 預印本/初次發布年份 (整數)
publication_year: 2017                                 # 正式出版/會議舉辦年份 (整數，若未正式出版填 null)
venue: "NeurIPS 2017"                                  # 正式發表會議或期刊名稱 (字串，若僅為預印本填 "arXiv")
doi: "10.5555/3295222.3295349"                         # 數位物件識別碼 (字串，無則填 null)
arxiv: "1706.03762"                                    # arXiv ID (字串，無則填 null)
url: "https://arxiv.org/abs/1706.03762"                # 官方發布或 arXiv 永久連結 (URL 字串)
pdf_file: "Papers/01 - Long Context & Sequence/(NeurIPS 2017-12) Attention Is All You Need.pdf" # 本地相對路徑
domains:                                               # 所屬專題領域 (List of Wikilinks)
  - "[[02 - 研究領域專題 (Research Domains)/Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)|Domain 01 - Long Context 與序列架構 (Attention, SSM, Ring)]]"
tags:                                                  # 標籤 (List of tags)
  - paper
  - dense-attention
verification_status: "verified"                        # 驗證狀態：verified (已比對原文全文) / pending_verification (待驗證) / abstract_only (僅摘要)
last_verified: 2026-09-24                              # 最後核對日期 (YYYY-MM-DD)
# 選填擴充欄位 (Optional Extended Metadata)：
artifact_type: "method_paper"                          # 工件類型：method_paper | benchmark_paper | dataset | evaluation_framework | survey | proposal
research_questions: []                                 # 探討之核心研究子題標籤 (如 retrieval_granularity, context_utilization)
benchmark_ids: []                                      # 相關之評測基準 ID
dataset_ids: []                                        # 相關之資料集 ID
metrics: []                                            # 評測指標
---
```

### 2. 論文筆記正文必備結構 (Mandatory Sections)
論文筆記正文**至少應完整包含以下 7 大核心板塊**。無法取得證據的項目應明確標註「待驗證」，**嚴禁為了填滿模板而主觀臆測或編造內容**：

1. **一話摘要 (TL;DR)**：一句話精準概括論文的核心貢獻與關鍵結論。
2. **研究背景與問題定義 (Problem Statement)**：原始作者試圖解決的核心痛點、現有方法瓶頸與研究假設。
3. **核心方法與技術架構 (Methodology & Architecture)**：具體演算法、數學公式、系統架構圖（Mermaid）與關鍵模組設計。
4. **主要實驗結果與證據 (Empirical Results & Evidence)**：
   - 記錄關鍵 Benchmark 分數；
   - **必須明確指出數據出處（如：Table 2, Page 6）**；
   - 註明評估之基準模型、Context 長度與硬體限制條件。
5. **優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)**：客觀剖析其技術代價（例如：計算量增加、顯存負擔、對特定任務的脆弱性）。
6. **對本專案研究領域的實際意義 (Implications for Research Domains)**：該技術在長文本處理、RAG、記憶體或長篇撰寫系統中的定位與借鑑價值。
7. **原始來源及相關筆記連結 (Sources & Related Notes)**：
   - 連結至本地 PDF：`[[Papers/...|開啟本地 PDF 檔案]]`；
   - 關聯之領域專題與同類/前驅/後繼論文筆記。

---

## ⚖️ 技術比較與 Trade-offs 規範 (Technical Comparisons & Trade-offs)

本知識庫嚴禁非學術性的「踩一捧一」或缺乏邊界的定性宣稱。在比較不同技術方案時，必須遵守以下規範：

### 1. 明確界定比較條件
針對以下典型技術對比（但不限於）：
- **Long Context vs. RAG**
- **Dense Retrieval vs. Sparse Retrieval**
- **GraphRAG vs. Conventional Vector RAG**
- **Transformer vs. State Space Models (SSM/Mamba)**

必須在報告與專題中逐一詳盡對比下列 6 大維度：
1. **適用任務與資料集**（Task & Dataset 特性，如 Factoid QA vs. Global Summarization vs. Multi-hop Reasoning）。
2. **模型規模及上下文長度**（Model Parameter Scale & Tested Context Length）。
3. **硬體資源與推論成本**（GPU 要求、FLOPs、API 成本）。
4. **記憶體需求、延遲及吞吐量**（KV Cache VRAM 佔用、Time-to-First-Token、Tokens/Second）。
5. **正確性、檢索品質及生成品質**（Recall, Precision, Faithfulness, Hallucination Rate）。
6. **方法的限制、失效情境與工程複雜度**（Failure Modes, Indexing Complexity, Maintenance Cost）。

### 2. 嚴格對照原則與禁令
- 🚫 **禁止無條件跨條件比較**：禁止將不同資料集、不同模型規模或不同評估條件下的分數直接作為技術優劣的證明。
- ⚠️ **明確標記「不可直接比較」**：若對比的兩組數據來自不同實驗環境，必須在表格與正文中明確醒目標註「不可直接比較（Incomparable Conditions）」，並陳述其變量差異。
- 🚫 **禁止過度推廣**：不得將特定實驗（如合成的單針大海撈針任務）的結果無條件推廣至所有實際使用情境。
- 💡 **技術建議必須附帶邊界條件**：任何技術選型推薦（如「何時選用 GraphRAG」）必須明確附帶其適用的先決條件、資源門檻與不適用場景。

---

## 📂 目錄結構規範 (Directory Structure Convention)

- `00 - 導覽與心智圖 (Navigation & MOC)/`：存放全景 MOC、主目錄與技術選型權衡筆記。
- `01 - 深度研究報告 (Deep Research Reports)/`：存放完整深度調研報告與對話存檔。
- `02 - 研究領域專題 (Research Domains)/`：存放各細分技術領域專題分析。
- `03 - 論文庫 (Literature Notes)/`：存放各篇論文標準化結構筆記，分類與檔名完全對齊 `Papers/` 結構：
  `03 - 論文庫 (Literature Notes)/[大類子資料夾]/(會議/期刊 發表年月) 論文名稱.md`
- `04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/`：存放尚未由既有文獻直接驗證的 taxonomy 延伸、研究假設、方法草案與實驗提案；**不得把這些內容寫成社群共識或已驗證方法**。
- `Papers/`：存放依大類分類的論文 PDF 全文，檔名格式統一為：
  `Papers/[大類子資料夾]/(會議/期刊 發表年月) 論文名稱.pdf`


---

## 🔎 Survey 與 Idea 分流規則 (Survey-vs-Idea Gate)

本 Repo 名稱為 RAG-survey，因此「Research Domains」中的分類與結論必須能由可追溯文獻支撐。

1. **Survey-backed domain**：每個 Domain 至少連到一篇與該領域直接相關的 survey / review / tutorial / benchmark overview；若目前找不到合適 survey，必須標示 `survey_coverage: partial`，不可假裝已有社群共識。
2. **Primary-paper evidence**：Survey 只能用來證明「這是一條已存在的研究線」；具體方法、數字與機制仍需回到 primary paper 核實。
3. **Ideas are not survey findings**：F/R/D/A/P/C/T、四層 Citation→Entailment→Authority→Sufficiency、Evidence Gap Controller、Temporal Conflict Resolver 等若沒有直接文獻證明其完整組合，必須放在 `04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/`，Research Domain 只能以「研究假設／設計草案」連結過去。
4. **禁止 novelty 宣告**：不得使用「唯一」「最高學術價值」「藍海」「已解決」「必然優於」等字眼，除非有明確、同條件、可追溯證據；研究價值應改寫成可反駁假設。
5. **Benchmark / Dataset / Metric 分離**：Benchmark 是任務與評測協議，Dataset 是資料，Metric 是計分方式，Evaluation Framework 是評估工具；不得混稱。

## 🧜 Mermaid 相容性規範

為同時相容 GitHub Mermaid 與 Obsidian：

- Mermaid node label **不得直接嵌入 Obsidian `[[wikilink]]`**；圖下方另設「圖中節點對照」使用 Wikilink。
- Node label 統一使用 `ID["文字"]` 或 decision `ID{"文字"}`；避免讓裸露的 `[` / `]` 出現在 label 中。
- HTML 換行統一使用 `<br/>`。
- `subgraph` 使用穩定 ID + 引號標題，例如 `subgraph retrieval["Retrieval Engine"]`。
- 不使用 `A & B --> C` 等 shorthand；拆成 `A --> C`、`B --> C`，提高不同 Mermaid renderer 的相容性。
- 修改 Mermaid 後必須至少檢查：fence 成對、node delimiter 成對、subgraph/end 成對，並確認 GitHub 預覽不顯示多餘的中括號。
