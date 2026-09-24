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
