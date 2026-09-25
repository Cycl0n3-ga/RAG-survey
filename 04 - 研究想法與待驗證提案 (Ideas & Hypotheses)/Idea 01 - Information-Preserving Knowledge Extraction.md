---
title: "Idea 01: Information-Preserving Knowledge Extraction"
evidence_status: "hypothesis"
tags:
  - idea
  - knowledge-extraction
  - rag
---

# Idea 01: Information-Preserving Knowledge Extraction for RAG

> [!WARNING]
> 這是本專案的 research hypothesis，不是既有 survey 共識。Generative IE surveys 支持 NER/RE/EE/UIE 的研究版圖；Dense X 等工作支持 proposition-level retrieval，但「Information-Preserving Extraction」作為 RAG 獨立問題仍需實證建立。

## 核心問題

結構化抽取提高可檢索性，但可能遺失：
- negation / modality；
- condition / exception；
- temporal validity；
- quantity / unit；
- provenance；
- cross-sentence dependency。

## 可反駁假設

> 在相同 retriever / generator 下，若 extraction representation 顯式保留 qualifier、condition、time、provenance，則 gold evidence recall、claim entailment 與 downstream QA/report factuality 應優於純 triple / decontextualized atomic-fact baseline。

## Baselines

- Raw chunk retrieval
- Sentence retrieval
- Dense X proposition retrieval
- Entity-relation triple retrieval
- Qualified proposition / evidence object（proposed）

## Oracle / Ablation

1. Gold extraction + same retrieval：隔離 extraction error。
2. Same extraction + gold retrieval：隔離 retrieval error。
3. 移除 time / condition / provenance 欄位：測各 qualifier 的邊際貢獻。
4. Cross-chunk consolidation on/off：測 entity resolution 與 temporal merge。

## Metrics

- Extraction precision / recall / F1
- Qualifier preservation rate
- Evidence recall@k
- Claim entailment
- Downstream answer correctness
- Error propagation rate

## 鄰接文獻

- Generative IE surveys：[[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]]
- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA|Dense X]]
- [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Contextualization|D02 Segmentation & Contextualization]]
