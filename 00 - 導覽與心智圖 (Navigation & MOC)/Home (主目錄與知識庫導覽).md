---
title: "RAG Survey Home"
tags:
  - moc
  - index
  - navigation
last_updated: "2026-10-02"
taxonomy_version: "v2"
---

# RAG Survey

> [!IMPORTANT]
> **如果目的是「閱讀這份 Survey」而不是查資料，請先讀：[[SURVEY|RAG Survey — Readable Synthesis]]。**
>
> 本 repo 的正式 taxonomy 仍是 **D01–D14**；GraphRAG / Hierarchical RAG / Agentic RAG 是 Paradigm Tags，Long Context / KV Cache / General Agents 等是 Adjacent Interfaces。

## Read the Survey

1. [[SURVEY|RAG Survey — From Knowledge Construction to Evidence-Grounded Generation (英文綜述主文)]]
2. [[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件閱讀與撰寫技術全景 (深度調研報告)|LLM 超長文件閱讀與撰寫技術全景 (正體中文旗艦深度調研報告)]]
3. [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy & Domain Map]]
4. [[00 - 導覽與心智圖 (Navigation & MOC)/RAG System Maps|RAG System Maps]]

> [!NOTE]
> `SURVEY.md` 與 `LLM 超長文件閱讀與撰寫技術全景 (深度調研報告).md` 是目前給人從頭讀到尾的主體綜述；下面的頁面則是支撐它們的研究資料庫。

## Research Database

1. [[02 - 研究領域專題 (Research Domains)/README|Research Domains]]
2. [[03 - 論文庫 (Literature Notes)/README|Literature Notes]]
3. [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|Benchmark Catalog]]
4. [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]]
5. [[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術全景與 Pareto 權衡分析 (Trade-offs)]]
6. [[00 - 導覽與心智圖 (Navigation & MOC)/Phase 1 Taxonomy Closure Audit - 2026-09-27|Phase 1 Taxonomy Closure Audit]]
7. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/README|Ideas & Hypotheses]]
8. [[00 - 導覽與心智圖 (Navigation & MOC)/GraphRAG Literature Coverage Gaps - 2026-10-02|GraphRAG 文獻缺口與候選閱讀清單（44 篇，全文待驗證）]]

## Simple Research Map

| Macro group | Domains | Central question |
|---|---|---|
| Source & Knowledge Construction | D01–D04 | 我們到底建立了什麼可檢索的知識物件？ |
| Retrieval & Evidence Control | D05–D08 | evidence 是否相關、足夠、可用且彼此一致？ |
| Grounded Generation | D09 | 哪些 claim 可以被 evidence 支持？ |
| Stateful & Agentic RAG | D10–D12 | 系統要維護什麼 state，下一步要做什麼？ |
| Evaluation | D13 | failure 真正發生在哪一層？ |
| Deployment & Trust | D14 | 能否有效率、安全地在真實環境運行？ |

完整 D01–D14 定義與邊界：[[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Taxonomy & Domain Map]]。

## Literature Corpus — Current Master Baseline

2026-10-02 已收錄筆記盤點（候選閱讀清單不計入）：

- **197** literature notes
- **143** notes have a D01–D14 `primary_domain`
- **54** notes are Adjacent/CROSS
- D01–D14 primary counts：5 / 5 / 19 / 9 / 29 / 7 / 6 / 9 / 8 / 1 / 8 / 6 / 22 / 9
- 已知 Phase 1 duplicate pairs 已完成 canonical-version cleanup

> [!WARNING]
> Literature storage folders 只是收納分類，**不是 Research Domains，也不是第二套 taxonomy**。

## Project Rules

```text
Domain = lifecycle / system research problem
Topic = subproblem inside a Domain
Paradigm Tag = cross-cutting method family
Adjacent Interface = related but non-core RAG research
Idea = project-specific hypothesis, not survey consensus

Segmentation != Extraction != Representation
Relevance != Sufficiency != Utilization != Faithfulness
Source/Index Maintenance != Persistent Derived Memory
```

## Current Reading Order

```text
SURVEY.md
   ↓
Taxonomy & Domain Map
   ↓
D01-D14 detailed Domain pages
   ↓
Representative Literature Notes
   ↓
Benchmark Catalog / Survey Papers / Audit Trail
```

這個順序刻意把「可閱讀的論述」和「可查證的研究資料庫」分開：先理解全貌，再往下鑽 paper-level evidence。
