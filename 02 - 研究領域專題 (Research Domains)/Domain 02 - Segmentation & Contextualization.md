---
title: "Domain 02 - Segmentation & Contextualization"
domain_id: "D02"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Corpus Construction"
last_updated: "2026-09-25"
---

# Domain 02 - Segmentation & Contextualization

> [!IMPORTANT]
> 本頁是目前正式 RAG Taxonomy v2 的 D02。核心只處理 retrieval unit 的切分與 contextualization；knowledge extraction 屬 D03，index design 屬 D04。

## Core Question
文件應被切成什麼 retrieval units，且切分後如何保留足夠上下文？如何在 **retrieval granularity、語意完整性、檢索效率、上下文保留** 之間取得可測量的平衡？

```mermaid
flowchart LR
    DOC["Structured Document"] --> SEG["Segmentation"]
    SEG --> FIX["Fixed / Recursive"]
    SEG --> SEM["Semantic / Structure-aware"]
    SEG --> FINE["Sentence / Proposition"]
    SEG --> PC["Parent-Child"]
    FIX --> U["Retrieval Units"]
    SEM --> U
    FINE --> U
    PC --> U
    U -. "optional" .-> C["Contextualization"]
    C --> D04["D04 Representation & Indexing"]
    U --> D04
    U -. "optional extraction" .-> D03["D03 Knowledge Extraction"]
```

## Includes
- fixed / recursive chunking
- semantic chunking
- structure-aware segmentation
- sentence / passage / proposition retrieval units
- parent-child segmentation
- contextualized chunks
- retrieval granularity
- segmentation-induced information loss

## Excludes
- entity / relation / event / claim extraction → [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Information Preservation|D03]]
- embedding / graph / index design → [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04]]
- query-time retrieval algorithm → [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|D05]]
- evidence sufficiency / retry / stopping → [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Adaptive Retrieval|D06]]

## Level-2 Topics
- Chunking
- Semantic Segmentation
- Structure-aware Segmentation
- Parent-Child Retrieval Units
- Proposition / Fine-grained Retrieval Units
- Contextualized Chunks
- Retrieval Granularity
- Segmentation Failure Analysis

## Boundary
```text
Segmentation != Knowledge Extraction != Knowledge Representation
```
Raw-chunk RAG 可由 D02 直接進 D04；D03 是可選支線，不是所有 RAG 的必要步驟。

## Representative Notes

**Current primary-note coverage: 3**

- [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA|Dense X]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2024-11) LumberChunker - Long-Context LLMs as Modular Chunkers for Long-Document RAG|LumberChunker]]
- [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-06) LongRAG - Enhancing Retrieval-Augmented Generation with Long-context LLMs|LongRAG]]

## Segmentation Strategies

| Family | Unit | Main trade-off |
|---|---|---|
| Fixed / token window | fixed token span | simple and cheap, but may cut semantic boundaries |
| Recursive | paragraph → sentence → token fallback | preserves some document hierarchy |
| Semantic | topic / semantic shift | better local coherence, higher preprocessing cost |
| Structure-aware | heading / section / table / list | uses document structure recovered by D01 |
| Proposition-level | atomic/self-contained statements | fine retrieval granularity but requires transformation/extraction |
| Parent-child | small retrieval unit + larger parent context | retrieval precision vs generation context |

## Contextualization Patterns & Exemplar Works

「Contextualization」不等於重新做 information extraction；它的目的是讓 retrieval unit 在脫離全文後仍保留足夠語境。

### 1. Contextual Chunk Representation：Late Chunking（D04 primary / D02 interface）
- Representative work: [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(arXiv 2024-09) Late Chunking - Contextual Chunk Embeddings for Retrieval|Late Chunking]]
- Late Chunking 的重點不是「重新做 IE」，而是解決傳統 chunking 破壞全域語意上下文的問題：
```text
whole-document encoding
        ↓
context-aware token representations
        ↓
chunk-level pooling
        ↓
contextualized chunk embeddings
```
- 因此它位於 D02 與 D04 的交界；但論文真正改動的是 **embedding representation**，故 Primary Domain = D04，D02 僅保留 contextualization interface。

### 2. Contextual Retrieval (Prepended Context)
- **Contextual Retrieval（Anthropic, engineering technique, 2024）**：為每個 chunk 產生簡短的 document-specific context，將其 prepend 到 chunk 後再建立 embedding 與 BM25 index。這是產業工程技術，不是本 repo 的 peer-reviewed paper note；官方說明：https://www.anthropic.com/engineering/contextual-retrieval。

### 3. Proposition Retrieval：Dense X
- Representative work: [[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(EMNLP 2024-11) Dense X - Exploring the Limit of Proposition Retrieval for Open-Domain QA|Dense X]]。
- 在本 taxonomy 中，Dense X 的 **Primary Domain = D02**，因為主要研究問題是 retrieval granularity。
- Proposition 的產生會碰到 D03，embedding/indexing 會碰到 D04，實際 ranking 會碰到 D05；因此它不是「Chunk → Proposition → Triple → Graph」的成熟度階梯。
- Proposition retrieval 的價值應以 benchmark 與 task 條件驗證，不應寫成已普遍取代 passage retrieval。

### 4. Semantic Chunking：LumberChunker
- Representative work: [[03 - 論文庫 (Literature Notes)/03 - RAG & Retrieval/(EMNLP 2024-11) LumberChunker - Long-Context LLMs as Modular Chunkers for Long-Document RAG|LumberChunker]]。
- 核心研究問題是：是否可用 long-context model 找出較符合語意轉折的 chunk boundaries，而不是固定 token window。其效益應在相同 retriever、相同 corpus 與相同 evaluation protocol 下比較。

### 5. Parent-Child / Section Context
- 以小 unit 檢索、用較大 parent context 提供生成內容，在檢索召回精度與生成上下文完整性之間取得平衡。

## Segmentation Failure Modes

- **Semantic fragmentation**：一個條件或推論被切到不同 units。
- **Dangling reference**：this system / the company / above requirement 失去 antecedent。
- **Qualifier separation**：數值與其 time / condition / modality 被切開。
- **Over-large units**：retrieval precision 下降、context noise 增加。
- **Over-small units**：跨句關係、條件與 discourse context 遺失。

> [!NOTE]
> 上述 failure modes 是研究問題分類，不代表存在一個跨所有資料集的固定失敗比例。

## Evaluation & Trade-offs for D02

D02 至少應同時觀察：
- retrieval Recall@k / Precision@k / nDCG
- downstream QA / task accuracy
- average unit length / number of units
- index size and preprocessing cost
- evidence boundary preservation
- cross-boundary failure rate
- parent-context expansion cost

只比較最終 answer accuracy 無法知道改善究竟來自 segmentation、retrieval 還是 generator。

## Structural Connections

```text
D01 Parsing / Structure
        ↓
D02 Segmentation / Contextualization
        ├──── raw retrieval units ───→ D04
        └──── semantic units ────────→ D03 (optional extraction)
                                         ↓
                                        D04
```

**Extraction is optional.** 傳統 chunk-based RAG 可直接由 D02 進 D04；只有需要 structured knowledge / graph / typed evidence 時才進 D03。

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Ingestion & Structure|D01 Document Ingestion & Structure]]
- [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Information Preservation|D03 Knowledge Extraction & Information Preservation]]
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Knowledge Representation & Indexing|D04 Knowledge Representation & Indexing]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy & Domain Map]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
