---
title: "Survey Papers Index"
tags:
  - survey
  - literature-map
  - rag
last_updated: "2026-09-24"
---

# Survey Papers Index

> [!IMPORTANT] Survey 判定規則
> 本 Vault 從此區分 **Survey / Review**、**Method Paper**、**Benchmark/Dataset Paper**、**Software/Framework**、**Project Idea**。  
> 只有有明確 survey/review 文獻支撐的領域級敘述，才標記為 **Survey-backed**。單篇方法論文只能支持該方法本身，不能自動證明整個 taxonomy 是社群共識。

## 1. General RAG

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Gao et al., *Retrieval-Augmented Generation for Large Language Models: A Survey* | arXiv 2023 | Naive / Advanced / Modular RAG、retrieval-generation pipeline |
| Wu et al., *Retrieval-Augmented Generation for Natural Language Processing: A Survey* (RAG and RAU) | arXiv 2024 | Retrieval-augmented understanding / generation across NLP |
| Zhao et al., *Retrieval-Augmented Generation for AI-Generated Content: A Survey* | Data Science and Engineering 2026 | RAG architectures、AIGC applications、evaluation / future directions |
| Brown et al., *A Systematic Literature Review of Retrieval-Augmented Generation: Techniques, Metrics, and Challenges* | BDCC 2025 | Systematic review、methods、metrics、challenges |

## 2. GraphRAG / Structured Knowledge

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Peng et al., *Graph Retrieval-Augmented Generation: A Survey* | ACM TOIS 2025 | GraphRAG taxonomy、graph construction、retrieval、generation、benchmarks |
| Zhong et al., *A Comprehensive Survey on Automatic Knowledge Graph Construction* | ACM Computing Surveys 2023 | KG construction；支撐 IE→KG，不等同 GraphRAG |

## 3. Information Extraction

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Xu et al., *Large language models for generative information extraction: a survey* | Frontiers of Computer Science 2024 | NER、RE、EE、Universal IE、LLM IE techniques |
| Zhang et al., *A Survey of Generative Information Extraction* | COLING 2025 | PLM/LLM generative IE、adaptation、generalization、unified IE |

> [!CAUTION]
> Proposition extraction、Information-Preserving Extraction、Extraction-to-RAG Error Propagation 目前不能因 Dense X 等單篇方法就宣稱為成熟 survey domain；後兩者保留在 Ideas。

## 4. Long Context / Context Engineering

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Wang et al., *Beyond the Limits: A Survey of Techniques to Extend the Context Length in Large Language Models* | IJCAI 2024 | context extension、architecture / training / extrapolation |
| Liu et al., *A Comprehensive Survey on Long Context Language Modeling* | arXiv 2025 | architecture、data、training、inference、evaluation |
| Liu et al., *Thus Spake Long-Context Large Language Model* | arXiv 2025 | architecture、infrastructure、training、evaluation |
| Mei et al., *A Survey of Context Engineering for Large Language Models* | arXiv 2025 | context retrieval、processing、management、agentic context |

## 5. Multimodal RAG

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Abootorabi et al., *Ask in Any Modality: A Comprehensive Survey on Multimodal Retrieval-Augmented Generation* | Findings of ACL 2025 | multimodal retrieval、fusion、generation、datasets、evaluation |

## 6. Evaluation / Trustworthiness / Faithfulness

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Yu et al., *Evaluation of Retrieval-Augmented Generation: A Survey* | CCF Big Data / Springer 2025 | RAG evaluation process、retrieval/generation metrics、benchmarks |
| Gan et al., *Retrieval Augmented Generation Evaluation in the Era of Large Language Models: A Comprehensive Survey* | arXiv 2025 | expanded evaluation taxonomy |
| Huang et al., *A Survey on Hallucination in Large Language Models* | ACM TOIS 2025 | factuality、faithfulness、detection、mitigation；含 RAG limitations |
| Li et al., *A Survey of Large Language Models Attribution* | arXiv 2023 | attribution / citation、sources、evaluation、limitations |
| Ni et al., *Towards Trustworthy Retrieval Augmented Generation for Large Language Models: A Survey* | ACM Computing Surveys 2026 | reliability、privacy、safety、fairness、explainability、accountability |

## 7. Agentic RAG

| Survey | 年份 / 狀態 | 支撐範圍 |
|---|---|---|
| Singh et al., *Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG* | arXiv 2025 | agentic RAG architectures、planning、tools、reflection、multi-agent |

## 8. Evidence status

每篇 literature note 建議加入：

```yaml
paper_type: "survey | method | benchmark | dataset | evaluation | software"
verification_status: "verified_from_paper | abstract_only | pending_verification"
evidence_scope: "這篇文獻實際能支持的敘述"
```

**禁止**把 `abstract_only` 寫成「已全文核實」，也禁止把 project hypothesis 標成 survey finding。

## 9. 原始來源入口

- Gao et al. RAG Survey: https://arxiv.org/abs/2312.10997
- Wu et al. RAG/RAU Survey: https://arxiv.org/abs/2404.19543
- Peng et al. GraphRAG Survey: https://doi.org/10.1145/3777378
- Xu et al. Generative IE Survey: https://doi.org/10.1007/s11704-024-40555-y
- Zhang et al. Generative IE Survey: https://aclanthology.org/2025.coling-main.324/
- Wang et al. Long Context Survey: https://doi.org/10.24963/ijcai.2024/917
- Liu et al. Comprehensive Long Context Survey: https://arxiv.org/abs/2503.17407
- Abootorabi et al. Multimodal RAG Survey: https://aclanthology.org/2025.findings-acl.861/
- Yu et al. RAG Evaluation Survey: https://arxiv.org/abs/2405.07437
- Huang et al. Hallucination Survey: https://doi.org/10.1145/3703155
- Li et al. Attribution Survey: https://arxiv.org/abs/2311.03731
- Ni et al. Trustworthy RAG Survey: https://arxiv.org/abs/2502.06872


## 補充：值得納入但仍需逐篇全文核驗的 survey candidates

下列項目用來擴充 coverage；在建立正式 Literature Note 前仍需核對作者、版本與正式 venue：

| Candidate | Coverage | Status |
| :--- | :--- | :--- |
| Retrieval-Augmented Generation for Natural Language Processing: A Survey | RAG / NLP taxonomy | pending_verification |
| A Survey on RAG Meeting LLMs: Towards Retrieval-Augmented Large Language Models | RAG pipeline / enhancement taxonomy | pending_verification |
| Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach | Long-context vs RAG（屬 comparative study，非純 survey） | primary_comparative_work |
| Long Context vs. RAG for LLMs: An Evaluation and Revisits | Long-context vs RAG（evaluation paper） | primary_comparative_work |
| Surveys on knowledge-graph / KG-enhanced RAG | Graph/KG RAG | pending_verification |
| Surveys on LLM memory mechanisms | Memory | pending_verification |
| Surveys on long-form text generation / report generation | Long-form generation | coverage_gap |

> [!CAUTION]
> 「更多 survey paper」不代表可以用 survey 取代 primary paper。Survey 用於建立研究領域與 taxonomy；演算法流程、作者聲稱、benchmark 數字、速度與成本仍應引用原論文。
