---
title: "Idea 02: Evidence Gap-Aware Adaptive Retrieval"
evidence_status: "hypothesis"
tags:
  - idea
  - adaptive-rag
  - evidence-sufficiency
---

# Idea 02: Evidence Gap-Aware Adaptive Retrieval

> [!WARNING]
> Adaptive-RAG、Self-RAG、IRCoT 等證明「何時檢索 / 如何迭代檢索」是可研究問題；但本頁提出的 **explicit evidence requirement → gap localization → targeted next action** controller 是 project hypothesis。

## 問題定義

不是只問「要不要再搜」，而是顯式表示：
1. 問題需要哪些 evidence requirements？
2. 現有 evidence set 已支持哪些？
3. 哪些 requirement 缺失、部分支持或互相衝突？
4. 下一步應 retrieve、re-extract、decompose、resolve conflict、abstain 還是 stop？

```mermaid
flowchart TD
    Q["Question"] --> REQ["Evidence Requirements"]
    REQ --> RET["Retrieve"]
    RET --> ASSESS{"Sufficiency / Conflict"}
    ASSESS -->|"missing"| GAP["Localize Evidence Gap"]
    GAP --> RET
    ASSESS -->|"conflict"| PROV["Provenance / Time Resolution"]
    ASSESS -->|"sufficient"| GEN["Grounded Generation"]
    ASSESS -->|"unresolvable"| ABS["Abstain / Ask for Source"]
```

## 可反駁假設

Gap-aware controller 應在相同 token / retrieval budget 下，提高：
- evidence coverage；
- answer correctness；
- citation completeness；
並降低不必要 retrieval calls。

## Baselines

- fixed top-k RAG
- IRCoT
- Self-RAG
- Adaptive-RAG
- query decomposition + fixed stopping

## Oracle

- gold decomposition
- gold evidence requirements
- gold gap labels
- gold stopping point

## Metrics

Evidence recall、requirement coverage、retrieval calls、latency/cost、answer correctness、abstention calibration。


## Evidence Slot State Model（project controller state）

> [!WARNING]
> 這是本專案 controller 的狀態設計，不等同於任何 benchmark 的官方 label set。

每個 required evidence slot 可處於：

1. `missing`：尚未找到候選證據。
2. `retrieved-unverified`：找到候選，但尚未完成 entailment / authority 驗證。
3. `supported`：已有足以支持該 requirement 的證據。
4. `conflicting`：存在互相矛盾的可用證據。
5. `ineligible`：內容相關，但因版本、authority、scope 或其他治理條件不能作為有效支持。

Action policy 不應只做 retrieve-more：
- missing → targeted retrieval；
- retrieved-unverified → verify；
- conflicting → D08 provenance/time resolution；
- ineligible → search alternate source；
- all required slots supported → stop / generate；
- budget exhausted → abstain / escalate。


## Stopping and Abstention Policy（proposed）

Evidence sufficiency 不應只是一個模糊的 0–1 self-score。對 requirement set (R(q)=\{r_1,...,r_m\}) 可定義 weighted coverage（本專案 proposed metric）：

[
Coverage(q,E)=\frac{\sum_i w_i s_i}{\sum_i w_i}
]

其中 (s_i=1) 表示 eligible evidence 已完整支持 requirement (r_i)。

建議 stopping 同時滿足：

[
Coverage \ge \tau_{cov}
]

[
CriticalMissing = 0
]

[
HighSeverityConflict = 0
]

並額外考慮：
- estimated marginal gain of another retrieval；
- remaining retrieval / token / latency budget。

### Abstention / downgrade cases

| Condition | Proposed action |
|---|---|
| critical evidence missing | abstain / partial answer |
| only stale evidence | explicitly state temporal limitation |
| only ineligible source | abstain / search alternate source |
| authoritative sources conflict | report conflict; do not guess |
| coverage below threshold | targeted retrieval; abstain after budget exhaustion |
| evidence retrieved but verifier cannot support claim | do not generate that claim |

### Metrics

- Evidence Slot Recall
- Critical Evidence Recall
- Counter-evidence Recall
- False-Sufficient Rate
- False-Insufficient Rate
- Early-stop Error Rate
- Abstention Accuracy
- Retrieval Rounds / Documents Read / Input Tokens / LLM Calls
