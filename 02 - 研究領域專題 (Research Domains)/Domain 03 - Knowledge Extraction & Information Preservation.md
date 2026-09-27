---
title: "Domain 03 - Knowledge Extraction & Consolidation"
domain_id: "D03"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Corpus Construction"
last_updated: "2026-09-27"
---

# Domain 03 - Knowledge Extraction & Consolidation

> [!WARNING]
> **Phase 1 closure is authoritative.** 若本頁較早段落與底部「Phase 1 Closure — 2026-09-27」衝突，以 closure 為準；舊文字暫留作 Phase 2 forensic audit，將於 Phase 7 一次正規化。

> [!IMPORTANT]
> 本 Domain 只回答：**從文字抽出什麼 semantic knowledge units，以及抽取、對齊與整合時如何避免失真？**
> Chunk boundary 本身屬 D02；knowledge representation / index schema 屬 D04。

## Core Question
應從原始內容抽取哪些語意知識單元，以及在進入 representation/indexing 前，如何完成必要的對齊、消歧與整合？

## Includes
- entity / relation / OpenIE / event extraction
- proposition / claim extraction
- coreference / entity resolution
- cross-chunk / cross-document consolidation
- extraction repair
- semantic fidelity：negation、modality、condition、temporal scope、quantity/unit、source scope、status

## Excludes
- retrieval-unit boundary → D02
- final vector / graph / index representation → D04
- query-time retrieval → D05
- evidence sufficiency controller → D06
- query-time evidence conflict resolution → D08

## Level-2 Topics
- Entity Extraction
- Relation Extraction / OpenIE
- Event Extraction
- Proposition / Claim Extraction
- Coreference / Entity Resolution
- Cross-chunk / Cross-document Consolidation
- Extraction Repair
- Semantic Fidelity / Information Preservation

## Boundary
**Retrieval Unit ≠ Semantic Unit.** Information Preservation 是 D03 的品質目標／research lens，而不是目前與 Extraction / Consolidation 同等成熟的獨立方法線。F/R/D/A/P/C/T 仍是本專案 hypothesis，不是既有 taxonomy 共識。

## Representative Notes

**Current primary-note coverage: 12**

- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2019-07) DocRED - A Large-Scale Document-Level Relation Extraction Dataset|DocRED]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2019-11) Entity, Relation, and Event Extraction with Contextualized Span Representations|DyGIE++]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2020-11) MAVEN - A Massive General Domain Event Detection Dataset|MAVEN]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2020-11) OpenIE6 - Iterative Grid Labeling and Coordination Analysis for Open Information Extraction|OpenIE6]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2022-05) Unified Structure Generation for Universal Information Extraction|UIE]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2023-04) InstructUIE - Multi-task Instruction Tuning for Unified Information Extraction|InstructUIE]]

## Extraction Targets

| Target | Typical output | Main risk |
|---|---|---|
| Entity | typed entity spans / IDs | entity boundary / linking error |
| Relation | subject-relation-object | missing qualifiers and document context |
| Event | trigger + arguments + time/status | event linking / temporal normalization |
| Proposition | atomic/self-contained statement | decontextualization loss |
| Claim | verifiable assertion | claim boundary / decomposition ambiguity |
| Typed record | schema-specific structured fields | schema mismatch / forced classification |

## UIE 與 Schema-guided Extraction 的邊界

UIE 類工作可支援「依 schema 抽取」的通用機制，但不代表它定義了本專案的 F/R/D/A/P/C/T ontology。

```text
Published mechanism:
(Text, Schema) -> Structured Extraction

Project-specific hypothesis:
Text -> F / R / D / A / P / C / T
     -> type-specific operational rules
```

F/R/D/A/P/C/T、其 operational semantics 與 evidence-governance pipeline 仍屬研究提案，不得在 Survey Domain 中表述為既有共識。

## Information Preservation (7 Qualifiers)

抽取正確不只代表 entity / relation label 正確；以下 qualifier 可能決定 statement 是否成立：
- **Negation**：否定條件與排除範圍
- **Modality**：必然、可能、建議、強制等語氣
- **Condition**：前置條件與適用情境（如「若...則...」）
- **Temporal scope**：時間區間、有效期限與生效日
- **Quantity & unit**：數值、度量衡與範圍邊界
- **Source scope**：陳述之觀點來源與引述範疇
- **Status**：狀態（如草案、定案、廢止、進行中）

簡單 SPO triple 可能無法表達這些 qualifier；是否改用 qualified triple、event、proposition、claim 或 evidence object 屬 D04 的 representation choice。

## Cross-chunk / Cross-document Consolidation

局部抽取後不能直接假定同名 entity、event 或 project status 已完成全局對齊。典型工作包括：
1. **coreference resolution**（代名詞與指代消解）
2. **entity linking / deduplication**（實體鏈結與去重）
3. **event linking**（事件對齊）
4. **temporal normalization**（相對時間轉絕對時間）
5. **source/version reconciliation**（來源與版本對齊）
6. **contradiction candidate detection**（潛在矛盾偵測）
7. **unsupported merge prevention**（防止無證據合併）

例如「Titan 團隊於 2024 年裁撤」不能自動合併成「Titan 專案於 2024 年終止」，除非另外有可支持該 inference 的 evidence。

與 GraphRAG 的交界：Cross-chunk extraction / augmentation 屬 D03；最終 graph schema/index 與 graph retrieval 分別屬 D04 / D05。

- Representative work: [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2026-05) Beyond Chunk-Local Extraction - Cross-Chunk Graph Augmentation for GraphRAG|CrossAug]]

## Extraction Repair & Error Propagation

Extraction failure 與 retrieval miss 不應混為一談：

```text
Source contains fact
      ↓
Extraction omitted / distorted fact
      ↓
Index never receives correct representation
      ↓
Retriever cannot recover it
```

因此 repair action 可能是：
- expand source window
- re-run extraction with alternate schema/prompt/model
- recover missing qualifier
- resolve entity/coreference
- compare against raw source span
- mark unresolved rather than hallucinate a merge

這類 failure 應與 D13 的 end-to-end failure attribution 一起評估。

## Evaluation Levels for D03

### 1. Extraction-level
- entity / relation / event Precision, Recall, F1
- proposition/claim extraction precision
- coreference / linking metrics
- qualifier preservation accuracy

### 2. Consolidation-level
- entity merge precision
- event-link accuracy
- temporal normalization accuracy
- unsupported-edge / unsupported-merge rate

### 3. RAG downstream
- evidence recall after extraction
- answer correctness / faithfulness
- error propagation under gold-vs-extracted knowledge

最後一組屬於 D13 的 evaluation protocol，而不是 D03 的方法本身。

## Structural Boundary with D02 and D04

```text
D02 Segmentation
      ↓ retrieval / source units
D03 Extraction & Preservation   [optional]
      ↓ semantic knowledge units
D04 Representation & Indexing
      ↓ searchable structures
D05 Retrieval
```

**Chunk、Proposition、Triple、Event、Graph 不構成單向成熟度鏈。**
它們可能分別是 retrieval unit、semantic unit、representation 或 index structure；分類時必須看 paper 的 primary contribution。

## Project Ideas
- [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 01 - Information-Preserving Knowledge Extraction|Idea 01 - Information-Preserving Knowledge Extraction]]
- [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 05 - Evidence-Governed RAG 系統架構構想 (Delta Pipeline Design)|Idea 05 - Evidence-Governed RAG 系統架構構想]]

## Consolidation Failure Modes
跨 chunk / cross-document consolidation 不只是「多抽一些 relation」；至少要防四類錯誤：

- **False merge / over-coreference**：不同實體被錯合併。
- **Unsupported edge**：跨段關係沒有 raw-span evidence 支持。
- **Qualifier cascade**：前一階段丟失 condition / time / negation，後續 multi-hop 將錯誤放大。
- **Extraction budget explosion**：為修復跨段關係反覆擴張 source window / re-extract，造成離線成本快速增加。

這些 failure 應與 Idea 01 的 information-preservation ablation 一起量測，而不是只看最終 QA accuracy。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Contextualization|D02 Segmentation & Contextualization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04 Knowledge Representation & Indexing]]
- [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/README|Ideas & Hypotheses]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy & Domain Map]]

## Phase 1 Closure — 2026-09-27

> [!IMPORTANT]
> **Canonical name: D03 Knowledge Extraction & Consolidation.**
> `Information Preservation` remains an important quality objective / research lens, but current literature does not justify treating it as an equally mature named research track.

**Core question**：應從原始內容抽取哪些語意知識單元，以及在進入 representation/indexing 前，如何完成必要的對齊、消歧與整合？

**Canonical scope**
- entity / relation / OpenIE / event extraction
- proposition / claim extraction
- coreference / entity resolution
- cross-chunk / cross-document consolidation
- semantic fidelity: negation, modality, condition, temporal scope, quantity/unit, source scope, status

**Boundary**
- retrieval unit ≠ semantic unit
- D02 chunking ≠ D03 extraction
- D04 representation/index ≠ D03 extraction
- D08 query-time evidence conflict ≠ D03 consolidation
- F/R/D/A/P/C/T remains a project-specific Idea/Hypothesis, not literature consensus

**Paper decisions**
- Keep the 12 current D03 anchors as extraction/consolidation coverage.
- CrossAug: D03 primary / D04 secondary; remove D05 secondary.
- Do not infer qualifier preservation merely from schema-valid output.
