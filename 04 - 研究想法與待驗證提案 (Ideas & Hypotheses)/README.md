---
title: "Ideas & Hypotheses"
tags:
  - ideas
  - hypotheses
  - proposed-method
last_updated: "2026-09-24"
---

# 研究想法與待驗證提案 (Ideas & Hypotheses)

> [!WARNING] 這裡不是 Survey 結論
> 本資料夾專門收納「有文獻鄰接證據，但尚未被 survey / 原始論文直接證明」的 taxonomy、研究假設、系統設計與 thesis proposal。  
> 任何內容若未找到足夠 survey / paper 支撐，不得搬回 Research Domains 當作既有共識。

## Evidence status

- `survey_backed`：有 survey/review 直接支持領域級敘述。
- `method_backed`：有原始方法論文支持方法，但不足以支持更廣泛 taxonomy。
- `proposed_method`：本專案提出的組合或 controller。
- `hypothesis`：可被實驗反駁的研究假設。
- `illustrative_only`：僅為例子，不可當 empirical result。
- `pending_verification`：名稱、數字、venue 或版本尚待官方來源核實。

## 目前 Ideas

1. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 01 - Information-Preserving Knowledge Extraction|Information-Preserving Knowledge Extraction]]
2. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 02 - Evidence Gap-Aware Adaptive Retrieval|Evidence Gap-Aware Adaptive Retrieval]]
3. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 03 - Provenance Temporal Conflict-Aware Evidence Resolution|Provenance / Temporal / Conflict-Aware Evidence Resolution]]
4. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 04 - End-to-End RAG Failure Attribution and Evidence Governance|End-to-End RAG Failure Attribution & Evidence Governance]]
5. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 05 - Evidence-Governed RAG 系統架構構想 (Delta Pipeline Design)|Evidence-Governed RAG 系統架構構想 (Delta Pipeline Design)]]
6. [[04 - 研究想法與待驗證提案 (Ideas & Hypotheses)/Idea 06 - 主流 RAG 框架生態與系統定位分析 (Framework Landscape & Positioning)|主流 RAG 框架生態與系統定位分析 (Framework Landscape & Positioning)]]

## 升格成 Survey-backed Domain 的門檻

- 至少一篇直接相關 survey/review，或多篇正式方法論文形成穩定文獻群；
- 清楚的 task definition；
- 可重現 baseline；
- benchmark / dataset / metrics；
- 能寫出可反駁假設，而不是只靠概念圖。


## Idea 05 / 06 的關係

- **Idea 05** 定義 Evidence-Governed Harness 的研究假設、F/R/D/A/P/C/T operational semantics、evidence hierarchy 與 deterministic repair loop。
- **Idea 06** 將 Idea 05 放入現有 RAG / Agent / Document-AI 工具生態中，區分「應借力的通用工程能力」與「需要以 ablation 驗證的核心研究假設」。
- Framework 的版本、功能與效能屬快速變動事實；Idea 06 的具體比較必須以官方文件或同條件 benchmark 定期重驗。
