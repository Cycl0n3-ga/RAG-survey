---
title: "補充資料與參考文獻評析 (Reference Audit)"
tags:
  - reference-audit
  - deep-research
---

> [!INFO] 導言
> 本文件記錄針對使用者補充之參考文獻所進行的系統性回查、文獻補強與架構評析。
> 深入剖析了從 **Chunk $\rightarrow$ Sentence $\rightarrow$ Proposition $\rightarrow$ Triple $\rightarrow$ Event $\rightarrow$ Graph** 的知識抽象階梯，並指出 Evidence Sufficiency 與 Cross-chunk Reasoning 的核心突破點。
> - **回主報告**：[[01 - 深度研究報告 (Deep Research Reports)/01 - LLM 超長文件閱讀與撰寫技術全景 (完整深度報告)|LLM 超長文件閱讀與撰寫技術全景報告]]
> - **相關專題**：[[02 - 研究領域專題 (Research Domains)/Domain 04 - Chunking 策略與知識擷取 (Proposition, Cross-chunk)|Chunking 策略與知識擷取]]

---

# 參考資料已收到：我會把它納入主研究版圖

## 這份資料的價值

這份 Markdown 很有用，因為它補強了前一版我還沒完整展開的 **RAG → Knowledge Representation → Graph/Memory → Evidence Reasoning** 這條支線。

我已讀到的內容大致涵蓋三組研究問題：

### RAG 本身不只是 Retrieval

資料把 RAG 拆成了幾個很值得保留的研究軸：

- **Knowledge Representation**：文件到底應該表示成 Chunk、Sentence、Proposition、Triple、Event，還是 Graph？
- **Evidence Sufficiency**：找到「相關」資料不代表資料已經「足夠」回答。
- **Adaptive RAG**：何時檢索、檢索幾次、什麼時候停止。
- **Context Utilization**：正確證據已經在 context 裡，LLM 為什麼仍然用錯或忽略？
- **Multi-hop Retrieval**：答案散落在多份文件、不同章節時如何建立 evidence chain。
- **Multimodal RAG**：文字、表格、圖片、圖表、PDF layout 如何一起檢索。
- **Faithfulness / Verification**：citation 存在不代表 citation 真的支持 claim。
- **Long-context vs. RAG Routing**：什麼時候整份直接讀，什麼時候應該 retrieval。

這個分類我會併入最後的 taxonomy，但會再往下細分成：

\[
\text{Document}
\rightarrow
\text{Representation}
\rightarrow
\text{Index}
\rightarrow
\text{Retrieve}
\rightarrow
\text{Expand}
\rightarrow
\text{Compress}
\rightarrow
\text{Reason}
\rightarrow
\text{Verify}
\rightarrow
\text{Write}
\]

這比單純的：

\[
\text{Retrieve}\rightarrow\text{Generate}
\]

更能描述現在真正的研究問題。

## 特別值得納入的 Knowledge Extraction 支線

你提供的資料裡，我認為最值得深入的是：

```text
Chunk
 │
 ├─ Raw Passage
 │
 ├─ Sentence
 │
 ├─ Proposition / Atomic Fact
 │
 ├─ Entity
 │
 ├─ Relation / Triple
 │
 ├─ Event
 │
 ├─ Claim
 │
 └─ Graph
      │
      ├─ Entity Graph
      ├─ Event Graph
      ├─ Evidence Graph
      └─ Community / Hierarchical Graph
```

而且這裡真正有研究價值的問題其實不是：

> 「Knowledge Graph 能不能比 Vector RAG 好？」

這已經太粗。

真正值得研究的是：

\[
\boxed{
\text{What information should be compressed into what representation?}
}
\]

例如原文：

> A 公司宣布將以五億美元收購 B 公司，但交易仍需主管機關核准。

如果壓成 triple：

```text
(A公司, 收購, B公司)
```

資訊其實已經壞掉了。

因為：

```text
宣布收購 ≠ 已完成收購
```

遺失的是：

- modality；
- temporal state；
- condition；
- uncertainty；
- provenance；
- transaction value；
- approval status。

因此我會把 **Knowledge Extraction 本身視為一種 Semantic Compression**。

也就是：

\[
\text{Raw text}
\xrightarrow{\text{Knowledge Extraction}}
\text{Compressed semantic representation}
\]

這會把你原先提出的兩個領域：

> Token Compression

以及：

> Knowledge Extraction

連成同一條更大的研究線：

```text
Compression
├── Surface compression
│   ├── token deletion
│   ├── prompt compression
│   └── sentence selection
│
├── Semantic compression
│   ├── summarization
│   ├── atomic propositions
│   ├── triples
│   ├── events
│   └── graphs
│
└── Latent compression
    ├── gist tokens
    ├── memory tokens
    ├── latent vectors
    └── compressed activations
```

這一點我會在完整報告中特別加強，因為我認為這是**目前很多文獻 taxonomy 沒有整理得非常乾淨的地方**。

## 這份資料提到的代表工作

我會逐篇回頭用**原始論文與官方專案**重新驗證，而不直接把這份 Markdown 當成 authoritative source。

目前資料中值得納入的核心 lineage 包括：

| 系統／論文 | 大方向 | 關鍵概念 |
|---|---|---|
| **Dense X Retrieval** | Retrieval granularity | Passage → Proposition |
| **Microsoft GraphRAG** | Graph RAG | Entity / Relation / Claim → Community |
| **HippoRAG** | Associative retrieval | OpenIE + knowledge graph + Personalized PageRank |
| **LightRAG** | Lightweight Graph RAG | Entity/Relation graph + dual-level retrieval |
| **KG²RAG** | Knowledge-guided retrieval | KG 用來擴展與組織 raw chunks |
| **HippoRAG 2** | Long-term non-parametric memory | Graph knowledge + original passages |
| **PropRAG** | Multi-hop proposition retrieval | Proposition path + beam search |
| **CrossAug** | Cross-chunk knowledge extraction | 補足 chunk-local extraction 漏掉的跨段關係 |

其中我尤其會把 **Dense X Retrieval → GraphRAG → HippoRAG → KG²RAG → PropRAG → Cross-chunk extraction** 畫成一條演化線。

大致可以理解成：

```text
Document chunk
    ↓
Dense Retrieval
    ↓
Smaller semantic units
    │
    ├── proposition
    ├── atomic fact
    └── triple
    ↓
Structured relationships
    ↓
Knowledge Graph
    ↓
Graph traversal / PPR / community
    ↓
Multi-hop evidence chain
    ↓
Cross-chunk reasoning
    ↓
Evidence-aware generation
```

## 我會再加一層：不要把「Chunk」當作天然存在的東西

這份參考資料已經碰到一個非常核心的問題，我會在正式整理時再往前推一步：

> **Chunking 本身其實就是一個 representation-learning 問題。**

傳統做法是：

\[
D
=
\{t_1,t_2,\dots,t_N\}
\]

每固定 \(k\) 個 token 切一次：

\[
C_i=
\{t_{ik},...,t_{(i+1)k-1}\}
\]

但這個切法跟文件裡真正的 knowledge boundary 沒有必然關係。

例如 datasheet：

```text
3.1 Electrical Characteristics
    VIH
    VIL
    IOH
    IOL

3.2 Timing Characteristics
    tSU
    tH
    tPD
```

固定 512-token chunk 很可能直接切在表格正中央。

更合理的 hierarchy 應該可能是：

```text
Document
└── Chapter
    └── Section
        ├── Paragraph
        ├── Table
        │   ├── Header
        │   ├── Row
        │   └── Footnote
        ├── Figure
        │   └── Caption
        └── Semantic Unit
            ├── Fact
            ├── Event
            ├── Constraint
            └── Relation
```

所以我會把 Chunking 從「RAG 前處理」提升成一個完整研究領域：

### Chunking research

```text
Chunking
├── Fixed-length
├── Sliding window
├── Sentence boundary
├── Paragraph boundary
├── Structure-aware
├── Semantic chunking
├── Topic segmentation
├── Proposition chunking
├── Query-aware chunking
├── Late chunking
├── Multi-resolution chunking
└── Learned / adaptive chunking
```

這會跟 **token compression、semantic compression、retrieval granularity** 三個領域直接接起來。

## 我會特別驗證幾個容易混淆的地方

你提供的資料很好當研究線索，但正式 deep research 報告裡，我不會直接照抄其中的年份、會議或效果數字。

尤其會逐項檢查：

1. **論文版本與正式發表版本是否一致。**  
   arXiv 日期、conference year、camera-ready year 常常不同。

2. **GraphRAG、HippoRAG、LightRAG 雖然都有 Graph，但研究問題不一樣。**  
   不能粗暴地把它們全部歸成同一種 KG-RAG。

3. **Atomic Fact、Proposition、Triple 並非等價表示。**

   可以粗略看成：

   \[
   \text{Triple}
   <
   \text{Atomic Fact}
   <
   \text{Proposition}
   <
   \text{Passage}
   \]

   左邊通常壓縮率較高、結構較強；右邊通常語境保留較完整。

4. **Graph retrieval 不一定優於 dense retrieval。**  
   很大程度取決於問題是否真的需要 relational / multi-hop structure，以及建圖誤差是否比 retrieval gain 更大。

5. **Knowledge extraction 有 error propagation 問題。**

   假設每個階段正確率：

   \[
   P_E=0.95
   \]

   entity linking：

   \[
   P_L=0.95
   \]

   relation extraction：

   \[
   P_R=0.90
   \]

   temporal/state extraction：

   \[
   P_T=0.90
   \]

   若一條完整 evidence path 必須四者都正確，一個非常粗略的獨立誤差模型會得到：

   \[
   P_{\text{path}}
   =
   0.95\times0.95\times0.90\times0.90
   \]

   \[
   P_{\text{path}}\approx0.731
   \]

   也就是個別模組看起來都「九成以上」，最後完整結構可能只剩約 **73%**。

   真實系統中各錯誤當然不是獨立的，因此這不能當實際預測值；但它很好地說明：

   > **Knowledge extraction 不是免費的壓縮。你是在用 representation compactness 換 error propagation risk。**

## 後續整合到完整研究圖的方式

我會把你這份資料放在整個版圖的這個位置：

```text
                     LONG DOCUMENT LLM
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
 MODEL CAPACITY       CONTEXT MANAGEMENT    EXTERNAL MEMORY
        │                   │                   │
 Long Context          Compression              RAG
 Efficient Attn        Chunking                  │
 Position              Selection                ├─ Retrieval
 Memory                 Summarization            │
        │                   │                   ├─ Knowledge Extraction
        │                   │                   │   ├─ Proposition
        │                   │                   │   ├─ Entity
        │                   │                   │   ├─ Relation
        │                   │                   │   ├─ Event
        │                   │                   │   └─ Claim
        │                   │                   │
        │                   │                   ├─ GraphRAG
        │                   │                   │
        │                   │                   ├─ Multi-hop
        │                   │                   │
        │                   │                   └─ Evidence Sufficiency
        │                   │
        └────────────┬──────┴───────────┬────────┘
                     │                  │
              REASONING LAYER      WRITING LAYER
                     │                  │
              Evidence Chain       Planning
              Verification         Section Memory
              Contradiction        Citation
              Tool Use             Revision
                     │                  │
                     └────────┬─────────┘
                              │
                      LONG-FORM OUTPUT
```

尤其會額外建立一條我認為很重要的統一軸：

\[
\boxed{
\text{Raw document}
\rightarrow
\text{Chunk}
\rightarrow
\text{Proposition}
\rightarrow
\text{Triple/Event}
\rightarrow
\text{Graph}
\rightarrow
\text{Latent Memory}
}
\]

它不是單純「不同 RAG 方法」，而可以視為：

> **資訊從高保真、低結構 → 高壓縮、高結構的 representation spectrum。**

這會是一個非常適合拿來組織整份 deep research 報告的核心框架。

我已經把這份 `/mnt/data/貼上的 Markdown (1)(20260922-060352).md` 納入後續整理；正式引用時會回到原論文、ACL/NeurIPS/ICML/ICLR proceedings、Microsoft/Google/Meta/OpenAI/Anthropic 等第一方資料逐項交叉驗證，而不把這份彙整稿本身當作論文證據。
