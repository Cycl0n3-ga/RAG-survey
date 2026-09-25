---
title: "Idea 03: Provenance / Temporal / Conflict-Aware Evidence Resolution"
evidence_status: "hypothesis"
tags:
  - idea
  - provenance
  - temporal-rag
  - conflict-resolution
---

# Idea 03: Provenance / Temporal / Conflict-Aware Evidence Resolution

> [!WARNING]
> Attribution、trustworthy RAG、temporal QA、fact checking 都有既有文獻；但把 valid time、recorded time、document version、source authority、counter-evidence 統一成 RAG evidence resolver，仍屬本專案 proposed direction。

## Evidence Object（proposed schema）

```yaml
evidence_id: E-001
claim_span: "..."
source_uri: "..."
source_hash: "..."
document_version: "..."
valid_time: "..."
recorded_time: "..."
authority: "primary | secondary | unknown"
stance: "support | contradict | neutral"
extraction_confidence: null
```

## 研究問題

- 新版文件與舊版文件衝突時，是否應以「最新」取代「最高權威」？
- valid time 與 recorded time 不一致時，回答應對哪個時間切片？
- 多來源互相矛盾時，系統如何保留 counter-evidence 而不是靜默平均？
- citation entailment 成立，但來源過期或低權威時，是否仍應輸出？

## 可反駁假設

在有版本衝突 / 時序更新 / source disagreement 的資料集上，顯式 provenance-time resolver 應優於「只以 retrieval score 排序」的 baseline。

## Metrics

Temporal accuracy、conflict detection F1、source selection accuracy、citation entailment、abstention / uncertainty calibration。


## Conflict Type Taxonomy（project lens）

為避免把所有矛盾都簡化成「新文件覆蓋舊文件」，至少區分：

1. **Temporal supersedence**：新版確實取代舊版。
2. **Scope divergence**：不同 site / condition / product / phase，表面矛盾但其實適用範圍不同。
3. **Authority discrepancy**：Draft / discussion note 與 Approved / authoritative source 衝突。
4. **Genuine contradiction**：相同時間、條件、scope 下仍不可調和。

## Candidate Resolution Policies

- **Recency heuristic**：只看新舊；成本低，但歷史問題與 draft 容易判錯。
- **Juxtaposition / disclosure**：保留多版本並列，不強行消解。
- **Provenance-aware arbitration**：依 authority、scope、valid time、version 做顯式仲裁。
- **Counter-evidence stress test**：將 support / contradict evidence 同時交給 verifier，檢查真正衝突來源。

這些是可比較的 resolution policies，不應把其中任何一種預設成普遍正確。
