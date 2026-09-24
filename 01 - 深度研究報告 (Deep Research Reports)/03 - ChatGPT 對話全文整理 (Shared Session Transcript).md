---
title: "ChatGPT 對話全文整理 (Shared Session Transcript)"
tags:
  - transcript
  - shared-chat
source_url: "https://chatgpt.com/share/6ab48c47-69b0-83e8-b415-014b1ca3180f"
---

# ChatGPT 對話全文整理 (Shared Session Transcript)

> [!NOTE] 對話背景
> - **原始分享連結**：[ChatGPT - 長文處理研究方向](https://chatgpt.com/share/6ab48c47-69b0-83e8-b415-014b1ca3180f)
> - **對話主題**：LLM 超長文件閱讀、理解、推理與長篇撰寫的完整研究方向
> - **包含模態**：使用者提問、初始 13 大主軸心智圖回答、使用者補充 Markdown 資料、兩輪 Deep Research 深度調研。

---

## 👤 使用者提問 (Turn 2)

LLM現在要怎麼解決一個非常長的文件閱讀與撰寫
請告訴我所有的研究方向 據我所知 現在可以研究long contect, token compress, context compress rag(retrieve, knowledge extraction...... 繼續計分)
請劃一個心智圖 告訴我現在大概都做什麼

---

## 👤 使用者提問 (Turn 6)

Original custom instructions no longer available

---

## 👤 使用者提問 (Turn 11)

LLM現在要怎麼解決一個非常長的文件閱讀與撰寫 請告訴我所有的研究方向 據我所知 現在可以研究long contect, token compress, context compress rag(retrieve, knowledge extraction...... 繼續細分) 請劃一個心智圖 告訴我現在大概都做什麼  

---

## 🤖 Assistant 回應 (Turn 13)

# LLM 如何解決超長文件的閱讀與撰寫？完整研究方向心智圖

這個問題可以拆成兩個不同的研究目標：

**長文件閱讀（Long-document Understanding）**：如何讓 LLM 從數十萬至數百萬 Token 的資料中，準確找到資訊、理解跨章節關係、整合證據，並回答複雜問題。

**長文件撰寫（Long-form Generation）**：如何讓 LLM 撰寫數萬字以上、前後一致、有完整結構、有事實依據，而且能持續修改的文件。

這兩件事情並不對稱。一個模型即使能讀入 1M Token，也不代表它能有效理解全部內容，更不代表它能一次寫出具有全局一致性的十萬字報告。

你提到的 Long Context、Token Compression、Context Compression、RAG、Knowledge Extraction，確實是重要研究方向，但還有幾個容易被忽略的領域：

- **Memory Architecture**：讓模型維護長期記憶，而不是每次重新閱讀全部文件。
- **Hierarchical Reasoning**：分層閱讀、規劃與推理，處理跨章節和跨文件依賴。
- **Long-form Generation**：以大綱、章節、迭代修訂及全局約束管理長篇寫作。
- **Context Engineering**：決定每個步驟要提供模型哪些資訊，而不只是擴大 Context Window。
- **Verification & Evaluation**：驗證模型是否真正讀懂文件、引用正確，以及長篇輸出有沒有自相矛盾。

以下把這些技術整理成研究分類樹，再進一步討論各分支的演算法、代表研究、適用場景，以及能如何組合成完整的長文件處理系統。



---

## 🤖 Assistant 回應 (Turn 23)

## 一、研究領域總覽：10 大主軸

這裡採用「依照要解決的問題」分類，而不是直接按照論文名稱分類。因為一篇論文可能同時屬於 RAG、Compression 和 Memory，這些技術並不是完全互斥的。

<box border radius="xl" gap={3} padding={3}>
  <box background="surface-secondary" radius="lg" padding={3} align="center">
    <title size="lg">Long-document Intelligence</title>
    <text color="secondary" size="sm">超長文件的理解、推理、記憶、生成與驗證</text>
  </box>
  <grid columns={2} gap={2}>
    {#each [{n:"01",t:"Long Context",d:"模型本身讀得更長",c:"#4775d1"},{n:"02",t:"Compression",d:"減少必須輸入的資訊量",c:"#b87732"},{n:"03",t:"RAG / Retrieval",d:"從外部文件找出相關證據",c:"#269b82"},{n:"04",t:"Knowledge Representation",d:"建立文件的結構與知識索引",c:"#9368c4"},{n:"05",t:"Memory Architecture",d:"跨步驟保留與更新資訊",c:"#c15e80"},{n:"06",t:"Hierarchical Reasoning",d:"分層理解與跨文件推理",c:"#5286a8"},{n:"07",t:"Long-form Generation",d:"分段撰寫、修訂與整合",c:"#bf843f"},{n:"08",t:"Agentic Workflow",d:"自主規劃工具與閱讀流程",c:"#6c9d53"},{n:"09",t:"Verification",d:"驗證引用、事實與一致性",c:"#c26861"},{n:"10",t:"Evaluation / Systems",d:"評測能力並控制運算成本",c:"#72829b"}] as b}
      <grid-item key={b.n} border radius="lg" padding={2} gap={1}>
        <row align="center" gap={2}>
          <box background={b.c} radius="sm" padding={{x:1,y:1}}>
            <text color="#ffffff" weight="semibold" size="xs">{b.n}</text>
          </box>
          <text weight="semibold" size="sm">{b.t}</text>
        </row>
        <text color="secondary" size="xs">{b.d}</text>
      </grid-item>
    {/each}
  </grid>
</box>

這 10 個主軸可再細分成數十個子領域。它們的關係可以理解成：

<box border radius="lg" padding={3} gap={2}>
  <box background="surface" radius="md" padding={2} align="center">
    <text weight="medium">原始文件：PDF、Word、表格、圖片、數百萬 Token</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    <text weight="medium">Document Parsing + Knowledge Representation</text>
    <text color="secondary" size="xs">辨識內容、結構、關係與來源位置</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <grid columns={2} gap={2}>
    <grid-item background="surface-secondary" radius="md" padding={2} align="center">
      **Long Context + Compression**
      <text color="secondary" size="xs">讓更多有效資訊進入模型</text>
    </grid-item>
    <grid-item background="surface-secondary" radius="md" padding={2} align="center">
      **RAG + Memory**
      <text color="secondary" size="xs">選擇、取得並維護需要的知識</text>
    </grid-item>
  </grid>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **Hierarchical Reasoning + Agentic Workflow**
    <text color="secondary" size="xs">分解任務、跨來源整合、規劃讀寫步驟</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2} align="center">
    **Long-form Generation + Verification**
    <text color="secondary" size="xs">逐章撰寫、反覆校驗、產出完整文件</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <text textAlign="center" color="success" weight="medium">可信賴、可追溯、跨章節一致的長篇文件</text>
  <caption>Evaluation 與 Systems Optimization 貫穿整個流程，用來測量品質、延遲、成本及資源使用量。</caption>
</box>

## 二、Long Context：讓模型本身讀得更長

Long Context 的研究目標不是把文件切成小塊，而是提高模型能直接處理的序列長度及長距離資訊利用能力。

<box gap={2}>
  <box border radius="lg" padding={3}>
    <badge color="info">1.1</badge>
    **Position Encoding & Context Extension**

    讓原本在較短序列上訓練的模型，能處理更長的位置範圍。

    - Position Interpolation / Extrapolation
    - RoPE Scaling、NTK-aware Scaling、YaRN
    - Long-context Continued Pretraining
    - Long-context Supervised Fine-tuning

    主要研究問題是位置編碼擴展後，原有的 Attention Pattern 是否仍然可靠。僅修改 RoPE 參數，不等於模型自動獲得長距離推理能力。<Cite refs={["turn858260search0","turn858260search7"]}/>
  </box>
  <box border radius="lg" padding={3}>
    <badge color="info">1.2</badge>
    **Efficient Attention**

    改善標準 Transformer 處理長序列所需要的運算量。

    - Exact Attention：FlashAttention 系列
    - Sparse Attention：Sliding Window、Block Sparse、Global Token
    - Linear Attention：以不同的 Attention 計算形式降低長序列成本
    - Distributed Attention：Sequence Parallelism、Ring Attention
    - Hybrid Attention：混合 Full / Sparse / Linear Attention

    重點：FlashAttention 主要改善實際記憶體讀寫與計算效率，並沒有把標準 Full Attention 的二次方運算複雜度直接變成線性。
  </box>
  <box border radius="lg" padding={3}>
    <badge color="info">1.3</badge>
    **Alternative Sequence Architectures**

    不完全依靠傳統 Full Attention 來處理長序列。

    - State Space Models：Mamba 系列
    - Recurrent Models：RWKV 等
    - Hybrid SSM–Transformer
    - Chunkwise Recurrent Processing
    - Recurrent Memory / Segment Recurrence

    研究取捨是：以較低的序列處理成本換取長距離建模能力時，能否維持對很久以前的特定細節進行精確檢索及推理的能力。
  </box>
  <box border radius="lg" padding={3}>
    <badge color="info">1.4</badge>
    **Long-context Learning & Reasoning**

    讓模型實際使用長文件資訊，而不只是允許輸入更多 Token。

    - Long-range Dependency Modeling
    - Lost-in-the-Middle / Position Bias
    - Multi-hop Reasoning Across Distant Passages
    - Distractor Robustness
    - Global Information Aggregation
    - Long-context Instruction Tuning

    這部分研究與長 Context Window 的硬體優化不同：前者改善理解能力，後者主要改善處理成本。
  </box>
</box>

### 為什麼 Context Window 不能一直無限制增加？

標準 Full Self-Attention 的核心計算是：

\[
\operatorname{Attention}(Q,K,V)
=\operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
\]

當序列長度為 \(N\) 時，\(QK^T\) 對應的 Attention Score Matrix 有 \(N\times N\) 個元素。

因此，在其他模型維度固定的情況下，核心 Attention 運算量隨長度約以 \(O(N^2)\) 成長。

<box border radius="lg" padding={3} gap={2}>
  <text weight="medium">序列長度增加，Attention 計算量如何變化？</text>
  <Chart content={{"chartType":"bar","meta":{"footer":"示意：假設模型架構與其他參數固定，僅改變序列長度。"},"xKey":"tokens","series":[{"dataKey":"relative","label":"相對運算量","valueSuffix":"×"}],"data":[{"tokens":"32K","relative":1},{"tokens":"64K","relative":4},{"tokens":"128K","relative":16},{"tokens":"256K","relative":64},{"tokens":"1M","relative":1024}]}}/>
</box>

此外，推論時的 KV Cache 通常隨 Context Length 線性增加：

\[
M_{\mathrm{KV}}
=2\times L\times N\times H_{\mathrm{KV}}
\times D_{\mathrm{head}}\times B
\]

其中 \(L\) 是 Transformer 層數、\(N\) 是已快取的 Token 數、\(H_{\mathrm{KV}}\) 是 KV Heads 數量、\(D_{\mathrm{head}}\) 是每個 Head 的維度，\(B\) 是每個元素的儲存位元組數。

因此，研究 Long Context 時應同時區分三件事：模型是否支援指定長度、模型能否正確使用該長度中的資訊，以及硬體能否負擔對應的運算與記憶體成本。



---

## 🤖 Assistant 回應 (Turn 30)

## 三、Compression：不是只有 Token Compression

這個方向最容易發生術語混淆。

「縮短文字」、「壓縮語意」、「減少 KV Cache」和「減少模型運算量」是四件不同的事。它們可以搭配使用，但不能視為相同的壓縮技術。

<box border radius="xl" padding={3} gap={3}>
  <title size="lg">Compression 研究分類樹</title>
  <box border radius="md" padding={3} gap={2}>
    <badge color="info">2.1 Input / Prompt Compression</badge>
    **縮短提供給模型的文字**

    <text size="sm">Token Pruning、Sentence Selection、Passage Selection、Extractive Compression、Abstractive Compression、Query-aware Compression、Query-agnostic Compression</text>

    代表研究：LLMLingua、LongLLMLingua、LLMLingua-2、EXIT。<Cite refs={["turn858260search8","turn858260search4","turn858260search1","turn858260search2"]}/>
  </box>
  <box border radius="md" padding={3} gap={2}>
    <badge color="info">2.2 Semantic / Latent Compression</badge>
    **把文字壓縮成較少的語意表示**

    <text size="sm">Soft Prompt、Learned Memory Tokens、Gist Tokens、Latent Bottleneck、Encoder–Decoder Compression、Learned Context Compressor</text>

    代表研究：500xCompressor，探索以少量特殊 Token 表示長篇上下文。<Cite refs={["turn180976search4"]}/>
  </box>
  <box border radius="md" padding={3} gap={2}>
    <badge color="info">2.3 KV Cache Compression</badge>
    **減少模型推論時保存的 Attention 狀態**

    <text size="sm">KV Quantization、KV Eviction、Token Merging、Head-aware Selection、Layer-aware Budget、Cache Offloading</text>

    代表研究：SnapKV、PyramidKV。<Cite refs={["turn757522search10","turn757522search2"]}/>
  </box>
  <box border radius="md" padding={3} gap={2}>
    <badge color="info">2.4 Memory / History Compression</badge>
    **縮短先前對話或 Agent 已經完成的工作歷程**

    <text size="sm">Rolling Summarization、Hierarchical Memory、Episodic Compression、Semantic Deduplication、State Compaction、Summary Refresh</text>
  </box>
  <box border radius="md" padding={3} gap={2}>
    <badge color="info">2.5 Document / Knowledge Compression</badge>
    **把整份文件壓縮為可查詢的知識表示**

    <text size="sm">Hierarchical Summarization、Proposition Extraction、Knowledge Graph、Topic Graph、Structured Tables、Document Synopsis</text>
  </box>
</box>

### 特別重要：Query-aware 與 Query-agnostic

假設一份文件有 100,000 Token。

如果使用者問：「第三章的功率消耗是多少？」

可以直接刪除與功耗無關的內容，這稱為 Query-aware Compression。對已知問題，這通常比較容易保留真正需要的資訊。

但如果使用者的要求是：「請完整理解文件，之後我會隨機問問題。」

就不能只保留功耗相關內容。此時需要 Query-agnostic Compression，或使用允許重新查閱原始文件的外部記憶架構。

可以把兩者的目標寫成：

\[
Z=C(X,Q)
\]

其中 \(X\) 是原始文件，\(Q\) 是當前問題，\(Z\) 是壓縮結果。這是 Query-aware Compression。

相對地：

\[
Z=C(X)
\]

則是在壓縮時不知道後續問題的 Query-agnostic Compression。

**兩者真正的研究難題是：如何在給定 Token Budget 內，盡可能保留後續任務所需要的資訊。**

另外，Compression Ratio 高並不直接等於效果好。真正需要測量的是壓縮後的答案正確率、資訊召回率及整體處理成本。

## 四、RAG：Retrieval 可以繼續細分到哪裡？

RAG 不應該被理解為單一演算法。它是一整套從資料建立、問題理解、查詢、檢索、資訊整合，到答案驗證的系統。

傳統的 Vector RAG 只是其中一種實作。

以下將它拆成八個階段。

<box border radius="xl" gap={3} padding={3}>
  <box background="surface-secondary" radius="md" padding={2}>
    <title size="lg">4.1 Document Ingestion & Parsing</title>
    <text color="secondary" size="sm">先把文件轉成機器可以檢索、推理的資料。</text>
  </box>
  <text weight="medium">Document Acquisition</text>
  <text size="sm">PDF / Word / HTML / 圖片 / 掃描文件 / 資料庫 / 程式碼 Repository</text>
  <divider color="subtle"/>
  <text weight="medium">Document Parsing</text>
  <text size="sm">OCR、Layout Analysis、Reading Order Detection、Table Extraction、Formula Recognition、Figure–Caption Linking、Footnote / Reference Parsing</text>
  <divider color="subtle"/>
  <text weight="medium">Document Structure Recovery</text>
  <text size="sm">Heading Hierarchy、Section Boundary、Parent–Child Relationship、Cross-reference、Page / Bounding-box Alignment、Document Versioning</text>
  <divider color="subtle"/>
  <text weight="medium">Multimodal Document Representation</text>
  <text size="sm">Text-based、Page-image-based、Layout-aware、Vision-language-based、Text–Image Joint Representation</text>
  <caption>這一層決定後續 RAG 有哪些資訊能夠使用。如果表格、公式或圖像在解析時遺失，再強的 Retriever 也找不回那些未被保存的資訊。多模態長文件研究已將跨頁、跨圖表推理列為重要評測對象。<Cite refs={["turn180976search2","turn180976search3"]}/></caption>
</box>

<box border radius="xl" padding={3} gap={3}>
  <title size="lg">4.2 Chunking：如何分割長文件？</title>
  <text color="secondary" size="sm">Chunking 不是單純每 512 Token 切一刀。</text>
  <table>
    <table-row><table-cell width="42%"><text weight="medium">Fixed-size</text></table-cell><table-cell>固定 Token / Character 長度</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Recursive</text></table-cell><table-cell>依段落、句子、分隔符逐級切分</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Semantic</text></table-cell><table-cell>依語意轉折或主題變化切分</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Structure-aware</text></table-cell><table-cell>依章節、標題、表格與附錄切分</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Parent–Child</text></table-cell><table-cell>小 Chunk 用於檢索，大 Chunk 用於回答</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Hierarchical</text></table-cell><table-cell>建立頁面、節、章、整份文件等多層級 Chunk</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Proposition-based</text></table-cell><table-cell>依單一事實、主張或命題切分</table-cell></table-row>
    <table-row><table-cell><text weight="medium">Contextualized</text></table-cell><table-cell>替 Chunk 補充標題、來源與周圍背景資訊</table-cell></table-row>
  </table>
  <text size="sm">Contextual Retrieval 的研究指出，獨立 Chunk 可能遺失原本的上下文，因此可以在建立檢索索引前，補充 Chunk 所屬文件及相關背景。<Cite refs={["turn628881search11"]}/></text>
</box>

<box border radius="xl" padding={3} gap={3}>
  <title size="lg">4.3 Indexing & Representation</title>
  <text color="secondary" size="sm">決定資訊如何儲存，以及檢索時如何比較相關性。</text>
  <grid columns={2} gap={2}>
    <grid-item border radius="md" padding={2}>
      **Lexical Index**
      <text size="sm" color="secondary">Inverted Index、BM25、Sparse Retrieval</text>
    </grid-item>
    <grid-item border radius="md" padding={2}>
      **Dense Index**
      <text size="sm" color="secondary">Embedding、Bi-encoder、Vector Database、ANN</text>
    </grid-item>
    <grid-item border radius="md" padding={2}>
      **Multi-vector Index**
      <text size="sm" color="secondary">Token-level Representation、Late Interaction、ColBERT</text>
    </grid-item>
    <grid-item border radius="md" padding={2}>
      **Structured Index**
      <text size="sm" color="secondary">Tree Index、Knowledge Graph、Entity Index、Metadata</text>
    </grid-item>
    <grid-item border radius="md" padding={2}>
      **Multimodal Index**
      <text size="sm" color="secondary">Page Embedding、Visual Embedding、Table Index、Cross-modal Index</text>
    </grid-item>
    <grid-item border radius="md" padding={2}>
      **Hybrid Index**
      <text size="sm" color="secondary">Sparse + Dense + Graph + Metadata</text>
    </grid-item>
  </grid>
  <text size="sm">Multi-vector Retrieval 與單一向量表示的不同之處，在於可以保留更細粒度的 Token-level 資訊，再進行 Late Interaction。ColBERTv2 是其中的代表研究。<Cite refs={["turn628881search3"]}/></text>
</box>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">4.4 Query Understanding & Transformation</title>
  <text color="secondary" size="sm">檢索前先理解使用者真正需要什麼。</text>
  <box gap={1}>
    <text weight="medium">Query Classification</text>
    <text size="sm">Factoid、Global Summary、Multi-hop、Comparison、Temporal、Numerical、Unanswerable Detection</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <text weight="medium">Query Rewriting / Expansion</text>
    <text size="sm">同義詞擴展、關鍵詞擷取、Hypothetical Document Embeddings（HyDE）、Query2Doc</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <text weight="medium">Query Decomposition</text>
    <text size="sm">Sub-question Generation、Multi-query、Dependency Planning、Step-back Prompting</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <text weight="medium">Query Routing</text>
    <text size="sm">選擇 BM25、Dense、Graph、SQL、全文閱讀或多模態檢索</text>
  </box>
</box>

<box border radius="xl" padding={3} gap={3}>
  <title size="lg">4.5 Retrieval Algorithms</title>
  <table>
    <table-row><table-cell width="43%">Sparse Retrieval</table-cell><table-cell>BM25、TF-IDF、SPLADE</table-cell></table-row>
    <table-row><table-cell>Dense Retrieval</table-cell><table-cell>Embedding 相似度、ANN Search</table-cell></table-row>
    <table-row><table-cell>Hybrid Retrieval</table-cell><table-cell>BM25 + Dense、RRF</table-cell></table-row>
    <table-row><table-cell>Hierarchical Retrieval</table-cell><table-cell>先找文件，再找章節、段落與原文</table-cell></table-row>
    <table-row><table-cell>Graph Retrieval</table-cell><table-cell>Entity Linking、Graph Traversal、Path Search、Community Search</table-cell></table-row>
    <table-row><table-cell>Multi-hop Retrieval</table-cell><table-cell>依據上一輪結果，搜尋下一段證據</table-cell></table-row>
    <table-row><table-cell>Adaptive Retrieval</table-cell><table-cell>動態選擇檢索方式、輪數和範圍</table-cell></table-row>
    <table-row><table-cell>Multimodal Retrieval</table-cell><table-cell>Text-to-Image、Page / Region / Table Retrieval</table-cell></table-row>
    <table-row><table-cell>Global Retrieval</table-cell><table-cell>檢索跨文件摘要、主題與社群層級資訊</table-cell></table-row>
  </table>
</box>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">4.6 Reranking & Evidence Selection</title>
  <text color="secondary" size="sm">第一階段找回大量候選內容後，選出真正值得送進生成模型的資訊。</text>
  <text size="sm">Cross-encoder Reranking、LLM Reranking、Pairwise / Listwise Reranking、Metadata Filtering、Deduplication、Diversity-aware Selection、Evidence Coverage、Sentence-level Selection、Budget-aware Packing。</text>
  <text weight="medium">重要差異</text>
  <text size="sm">Reranking 是重新排序候選證據；Context Compression 是刪減或重寫證據內容。兩者可以串接使用。</text>
</box>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">4.7 Context Construction / Fusion</title>
  <text color="secondary" size="sm">檢索到的資訊不一定要直接串接成一段 Prompt。</text>
  <text size="sm">Context Packing、Position-aware Ordering、Evidence Grouping、Hierarchical Summarization、Map–Reduce Synthesis、Multi-document Fusion、Conflict Resolution、Citation-aware Synthesis、Adaptive Token Budget。</text>
</box>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">4.8 Retrieval Feedback & Verification</title>
  <text color="secondary" size="sm">如果找到的證據不足，系統能否自行重新搜尋？</text>
  <text size="sm">Retrieval Confidence Estimation、Evidence Sufficiency、Corrective Retrieval、Self-reflection、Answerability Detection、Citation Verification、Query Reformulation、Iterative Retrieval。</text>
  <text size="sm">Self-RAG 探索依需求檢索與自我評估；這與每次固定取回 Top-k Chunk 的流程不同。<Cite refs={["turn628881search5","turn628881search10"]}/></text>
</box>

### RAG 研究中，四個值得特別分清楚的方向

<box gap={3}>
  <row align="start" gap={3}>
    <AsyncImage query="RAPTOR recursive abstractive processing tree organized retrieval diagram paper" aspectRatio="1:1" maxWidth="86px"/>
    <box flex="1" gap={1}>
      **<Entity category="scientific_concept" value="RAPTOR" disambig="Recursive Abstractive Processing for Tree-Organized Retrieval"/>**

      核心：將 Chunk 聚類、摘要，再遞迴建立多層級樹狀索引。檢索可以同時利用原文與不同抽象程度的摘要。

      適合研究如何讓長文件兼具局部細節與全局理解。<Cite refs={["turn628881search0"]}/>
    </box>
  </row>
  <divider color="subtle"/>
  <row align="start" gap={3}>
    <AsyncImage query="Microsoft GraphRAG knowledge graph community summaries architecture diagram" aspectRatio="1:1" maxWidth="86px"/>
    <box flex="1" gap={1}>
      **<Entity category="scientific_concept" value="GraphRAG" disambig="Graph-based Retrieval-Augmented Generation"/>**

      核心：抽取實體與關係、建立知識圖譜、產生 Community Summaries，支援局部及全局查詢。

      適合研究跨章節關係、跨文件問題與全局性主題分析。<Cite refs={["turn628881search1","turn628881search9"]}/>
    </box>
  </row>
  <divider color="subtle"/>
  <row align="start" gap={3}>
    <AsyncImage query="LightRAG simple and fast retrieval augmented generation dual level retrieval architecture" aspectRatio="1:1" maxWidth="86px"/>
    <box flex="1" gap={1}>
      **<Entity category="scientific_concept" value="LightRAG" disambig="Lightweight knowledge graph and vector retrieval framework"/>**

      核心：結合圖結構與向量檢索，設計低層級與高層級的雙層檢索方式。

      適合研究圖譜與向量索引的混合式資訊檢索。<Cite refs={["turn628881search4"]}/>
    </box>
  </row>
  <divider color="subtle"/>
  <row align="start" gap={3}>
    <AsyncImage query="Self RAG learning retrieve generate critique self reflection architecture diagram" aspectRatio="1:1" maxWidth="86px"/>
    <box flex="1" gap={1}>
      **<Entity category="scientific_concept" value="Self-RAG" disambig="Self-Reflective Retrieval-Augmented Generation"/>**

      核心：模型學習何時需要檢索，並評估檢索內容與生成結果。

      適合研究動態檢索策略、模型自我評估，以及答案與證據的一致性。<Cite refs={["turn628881search5"]}/>
    </box>
  </row>
</box>

四者可以結合使用。例如，用 RAPTOR 管理文件層級，用 GraphRAG 保存實體關係，再使用 Self-RAG 式的策略決定什麼時候需要進一步取得證據。

但實際效益必須由目標資料集驗證。知識圖譜不是對任何文件、任何問題都比基本 Vector RAG 有利。



---

## 🤖 Assistant 回應 (Turn 34)

## 五、Knowledge Representation & Extraction：讓文件變成真正可用的知識

這個領域與 RAG 有密切關係，但不是完全相同。

RAG 研究的是如何取得外部知識；Knowledge Representation 研究的是知識應該如何表示、組織與保存。

如果只把文件轉換成一組 Embedding，原始文件中的階層、順序、數字、因果和引用關係，不一定都能被完整保留。

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">5.1 Knowledge Extraction</title>
  <text color="secondary" size="sm">將非結構化文件轉換為結構化資訊。</text>
  <box gap={1}>
    **Entity-level Extraction**

    <text size="sm">Named Entity Recognition（NER）、Entity Linking、Coreference Resolution、Entity Disambiguation、Entity Resolution</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    **Relation-level Extraction**

    <text size="sm">Relation Extraction、Event Extraction、Temporal Relation、Causal Relation、Multi-hop Relation</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    **Fact / Claim Extraction**

    <text size="sm">Atomic Fact Extraction、Proposition Extraction、Claim–Evidence Alignment、Condition / Exception Extraction、Negation Detection</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    **Domain-specific Extraction**

    <text size="sm">Scientific Knowledge Extraction、Financial Information Extraction、Legal Clause Extraction、Technical Specification Extraction、Numerical Fact Extraction</text>
  </box>
</box>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">5.2 Knowledge Representation</title>
  <text color="secondary" size="sm">將抽取出的內容建立成可供推理與查詢的形式。</text>
  <table>
    <table-row><table-cell width="43%">Semantic Representation</table-cell><table-cell>Dense Embedding、Multi-vector、Learned Latent Representation</table-cell></table-row>
    <table-row><table-cell>Structured Representation</table-cell><table-cell>JSON、Schema、Entity–Attribute–Value、Relational Table</table-cell></table-row>
    <table-row><table-cell>Graph Representation</table-cell><table-cell>Knowledge Graph、Property Graph、RDF、Ontology</table-cell></table-row>
    <table-row><table-cell>Hierarchical Representation</table-cell><table-cell>Document Tree、Topic Tree、Summary Tree</table-cell></table-row>
    <table-row><table-cell>Temporal Representation</table-cell><table-cell>Temporal KG、Versioned Facts、Event Timeline</table-cell></table-row>
    <table-row><table-cell>Provenance Representation</table-cell><table-cell>Source ID、Page / Span、Evidence Link、Confidence、Extraction Method</table-cell></table-row>
  </table>
</box>

### 這類研究真正值得深挖的地方：如何保留「條件」與「例外」？

例如，文件內容是：

> 當輸入電壓大於 12 V，且溫度低於 80°C 時，系統最高支援 5 A；但在低功耗模式下，最大電流限制為 2 A。

如果 Knowledge Extraction 只產生：

`(System, MaxCurrent, 5A)`

那麼就已經遺失了正確解讀這個規格所必需的條件。

更完整的表示應接近：

```json
{
  "subject": "System",
  "property": "max_current",
  "value": 5,
  "unit": "A",
  "conditions": {
    "input_voltage": ">12V",
    "temperature": "<80C",
    "operating_mode": "normal"
  },
  "exception": {
    "operating_mode": "low_power",
    "max_current": "2A"
  },
  "source": {
    "document": "datasheet.pdf",
    "page": 18,
    "section": "Electrical Characteristics"
  }
}
```

這個例子是示意資料，不是實際元件規格。

對工程規格書、法律條文、科學文獻與財務文件來說，**條件、否定、例外、時間與來源資訊都可能是知識本身不可分割的一部分。**

因此，可以研究 Condition-aware Knowledge Extraction、Evidence-preserving Extraction，以及支援文件修訂的 Temporal Knowledge Representation。

## 六、Memory Architecture：讓模型不必每次重新讀完整份文件

Memory 與 Long Context 的主要差別是：

Long Context 讓模型一次看到更多資料；Memory 讓模型在多次操作之間，持續保存、更新與重新取得資訊。

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">Memory 研究分類</title>
  <box gap={1}>
    <badge>6.1 Working Memory</badge>
    <text size="sm">目前問題、最近閱讀的段落、暫時推理結果、當前章節草稿、Active Context Management。</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge>6.2 Episodic Memory</badge>
    <text size="sm">先前閱讀紀錄、檢索歷史、已完成任務、使用者修訂紀錄、決策過程摘要。</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge>6.3 Semantic Memory</badge>
    <text size="sm">從文件抽取的事實、概念、實體關係、知識圖譜、整體文件知識庫。</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge>6.4 Procedural Memory</badge>
    <text size="sm">寫作規範、報告格式、研究步驟、工具使用策略、文件處理程序。</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge>6.5 Memory Management</badge>
    <text size="sm">Memory Write / Read / Update / Delete、Salience Scoring、Deduplication、Forgetting、Consolidation、Conflict Detection、Version Control。</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge>6.6 Hierarchical / Virtual Memory</badge>
    <text size="sm">多層記憶、外部儲存、動態載入、不同記憶層之間的資訊交換、Context Paging。</text>
  </box>
</box>

<row align="start" gap={3}>
  <AsyncImage query="MemGPT virtual context management hierarchical memory architecture paper diagram" aspectRatio="1:1" maxWidth="86px"/>
  <box flex="1" gap={1}>
    **<Entity category="scientific_concept" value="MemGPT" disambig="Virtual context management for language models"/>**

    2023 年提出的研究，借鑑作業系統的階層式記憶體管理，讓 LLM 在有限的 Context Window 中管理更大規模的外部資訊。<Cite refs={["turn4search0"]}/>
  </box>
</row>

<row align="start" gap={3}>
  <AsyncImage query="A Mem Agentic Memory for LLM Agents Zettelkasten NeurIPS 2025 memory graph diagram" aspectRatio="1:1" maxWidth="86px"/>
  <box flex="1" gap={1}>
    **<Entity category="scientific_concept" value="A-Mem" disambig="Agentic Memory for LLM Agents"/>**

    NeurIPS 2025 的研究，探索如何動態建立記憶之間的連結，以及新增資訊後如何更新既有記憶的組織與描述。<Cite refs={["turn4search1"]}/>
  </box>
</row>

Memory 最值得研究的問題之一，是當文件新增一項資訊或修訂某個章節時，系統該如何更新既有知識。

例如原始文件說最大電流為 5 A，修訂版改成 4 A。不能只把 4 A 當作另一個記憶加入，然後讓模型隨機檢索到其中一個數值；系統需要辨識版本、有效時間與事實的覆蓋關係。

## 七、Hierarchical Reasoning：跨章節、跨文件的真正理解

假設使用者要求：

「閱讀 300 篇論文，分析各方法在成本、準確率與可擴展性上的共通限制，並提出新的研究方向。」

這不是簡單的 Top-k 檢索問題，因為答案需要綜合整個資料集合。

研究方向可以繼續分成：

<box border radius="lg" padding={3} gap={2}>
  <text weight="medium">7.1 Hierarchical Understanding</text>
  <text size="sm">段落理解 → 章節理解 → 文件理解 → 跨文件整合。包括 Bottom-up Summarization、Top-down Refinement、Recursive Abstraction。</text>
  <divider color="subtle"/>
  <text weight="medium">7.2 Multi-hop Reasoning</text>
  <text size="sm">需要串接不同來源的證據才能回答問題。包括 Evidence Chain、Graph Traversal、Iterative Retrieval、Reasoning Path Planning。</text>
  <divider color="subtle"/>
  <text weight="medium">7.3 Global Reasoning</text>
  <text size="sm">跨整個文件集合的主題發現、分類、比較、趨勢分析、完整性檢查與資訊聚合。</text>
  <divider color="subtle"/>
  <text weight="medium">7.4 Cross-document Reasoning</text>
  <text size="sm">Cross-document Entity Resolution、Contradiction Detection、Temporal Alignment、Evidence Aggregation、Consensus / Disagreement Analysis。</text>
  <divider color="subtle"/>
  <text weight="medium">7.5 Planning-based Reasoning</text>
  <text size="sm">將複雜問題拆成可執行子問題，建立相依關係，按順序或平行取得證據，再整合為最後答案。</text>
</box>

這個領域與 GraphRAG、RAPTOR、Memory 和 Agentic RAG 高度重疊，但其研究核心是「推理流程」，而不是索引格式本身。



---

## 🤖 Assistant 回應 (Turn 35)

## 八、Long-form Generation：如何讓 LLM 寫出數萬字的文件？

這是整個領域中，最不應該被 Long Context 研究掩蓋的問題。

2025 年 ICLR 的 LongWriter 研究指出，模型即使可以接收很長的輸入，也可能難以產生同等長度的高品質輸出。該研究透過 AgentWrite 將長篇寫作拆解為多個子任務，並研究長輸出資料訓練。<Cite refs={["turn0search3"]}/>

2026 年 ACL 的 IS-CoT 進一步研究在生成過程中動態交替規劃、寫作與反思，以改善長篇生成時的結構和篇幅問題。<Cite refs={["turn4search20"]}/>

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">Long-form Generation 研究分類樹</title>
  <box gap={1}>
    <badge color="info">8.1 Planning & Outlining</badge>
    <text size="sm">Hierarchical Outline、Chapter Planning、Content Allocation、Dependency Graph、Outline Refinement、Length Budgeting</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.2 Long-output Model Training</badge>
    <text size="sm">Long-output SFT、Long-form Preference Optimization、Length Control、Long-form Coherence Training</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.3 Iterative / Incremental Writing</badge>
    <text size="sm">Section-wise Generation、Progressive Drafting、Plan–Write–Reflect、Coarse-to-Fine Generation、Continuation</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.4 Retrieval-grounded Writing</badge>
    <text size="sm">Evidence-first Writing、Chapter-specific Retrieval、Claim–Evidence Binding、Citation-aware Generation、Gap-aware Retrieval</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.5 Global Coherence</badge>
    <text size="sm">Entity Consistency、Terminology Consistency、Cross-chapter Dependency、Narrative Continuity、Global Constraint Tracking</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.6 Revision & Editing</badge>
    <text size="sm">Self-revision、Critique–Revise、Targeted Editing、Cross-section Revision、Document-level Editing、Version-aware Regeneration</text>
  </box>
  <divider color="subtle"/>
  <box gap={1}>
    <badge color="info">8.7 Controlled & Structured Generation</badge>
    <text size="sm">Schema-constrained Writing、Template Following、Style Consistency、Section-specific Rules、Numerical Consistency、Document Assembly</text>
  </box>
</box>

### 實務上，長篇寫作應有獨立的 Evidence Store 和 Document State

假設目標是根據 100 篇論文，產生一份 30,000 字的技術報告。

不要只讓模型看一份摘要，然後要求它一次寫出完整報告。可以設計成：

<box border radius="lg" padding={3} gap={2}>
  <box background="surface-secondary" radius="md" padding={2} align="center">
    **Global Plan**
    <text color="secondary" size="sm">報告目的、目錄、章節關係、篇幅分配</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **Evidence Store**
    <text color="secondary" size="sm">研究主張、數據、來源、引用位置、可回溯原文</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **Chapter Writer**
    <text color="secondary" size="sm">按章節取得相關證據，逐節生成內容</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **Document State**
    <text color="secondary" size="sm">已完成段落、重要定義、術語、跨章節相依性</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **Global Editor**
    <text color="secondary" size="sm">檢查前後一致、章節重複、證據缺漏與引用問題</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface" radius="md" padding={2} align="center">
    **Final Document**
    <text color="secondary" size="sm">合併、格式處理、交叉引用、輸出與驗證</text>
  </box>
</box>

2026 年的 EviReport 研究採用了與此相關的方向，包括可追溯證據單元、階層式大綱，以及由事實驅動的反覆寫作與證據補充流程。<Cite refs={["turn4search39"]}/>

## 九、Agentic Workflow：讓模型自己決定下一步應該做什麼

Agentic RAG 不只是呼叫一次 Retriever，而是讓模型根據任務進展，決定是否要繼續閱讀、重新搜尋、壓縮資訊、修訂內容或呼叫外部工具。

<box border radius="lg" padding={3} gap={2}>
  <text weight="medium">主要研究方向</text>
  <table>
    <table-row><table-cell width="42%">Task Planning</table-cell><table-cell>任務分解、子問題規劃、動態更新執行計畫</table-cell></table-row>
    <table-row><table-cell>Tool Selection</table-cell><table-cell>選擇全文搜尋、向量檢索、Graph Search、SQL、Python 等工具</table-cell></table-row>
    <table-row><table-cell>Adaptive Retrieval</table-cell><table-cell>決定何時檢索、檢索多少次，以及何時停止</table-cell></table-row>
    <table-row><table-cell>Reflection</table-cell><table-cell>檢查資訊是否充足、是否需要補充證據</table-cell></table-row>
    <table-row><table-cell>Multi-agent Collaboration</table-cell><table-cell>Reader、Retriever、Writer、Reviewer 等角色協作</table-cell></table-row>
    <table-row><table-cell>Workflow Optimization</table-cell><table-cell>控制工具呼叫次數、Token Budget、延遲及停止條件</table-cell></table-row>
    <table-row><table-cell>Persistent Workspace</table-cell><table-cell>維護文件進度、研究筆記、草稿、引用與執行狀態</table-cell></table-row>
  </table>
</box>

其中，是否需要多個 Agent，應該當成研究問題，而不是預設答案。

單一 Agent 搭配結構化工具和明確的狀態管理，也能完成複雜的閱讀與寫作任務。多個 Agent 可能改善任務分工，但同時也會增加通訊、上下文同步與錯誤傳遞的成本。

## 十、Verification & Evaluation：模型真的讀懂、寫對了嗎？

長文件系統不能只用「答案看起來合理」作為驗收標準。

至少需要分開評估六種能力：

<box border radius="xl" padding={3} gap={2}>
  <title size="lg">10.1 Verification：輸出品質驗證</title>
  <text size="sm">Groundedness、Factual Consistency、Citation Accuracy、Claim Verification、Numerical Verification、Contradiction Detection、Coverage Verification、Faithful Summarization。</text>
  <divider color="subtle"/>
  <title size="lg">10.2 Retrieval Evaluation</title>
  <text size="sm">Recall@k、Precision@k、MRR、nDCG、Evidence Recall、Evidence Sufficiency、Retrieval Cost。</text>
  <divider color="subtle"/>
  <title size="lg">10.3 Long-context Evaluation</title>
  <text size="sm">Single / Multi-needle Retrieval、Position Robustness、Multi-hop Reasoning、Global Aggregation、Distractor Robustness、Long-context Instruction Following。</text>
  <divider color="subtle"/>
  <title size="lg">10.4 Long-form Generation Evaluation</title>
  <text size="sm">Length Compliance、Content Coverage、Global Coherence、Redundancy、Citation Coverage、Cross-section Consistency、Style Consistency。</text>
  <divider color="subtle"/>
  <title size="lg">10.5 Multimodal Document Evaluation</title>
  <text size="sm">Page / Region Retrieval、Table Reasoning、Chart Interpretation、Figure-grounded QA、Cross-page Evidence Integration。</text>
  <divider color="subtle"/>
  <title size="lg">10.6 Systems Evaluation</title>
  <text size="sm">TTFT、Prefill Throughput、Decode Throughput、Peak VRAM、KV Cache Usage、End-to-end Latency、Indexing Cost、Cost per Correct Answer。</text>
</box>

代表性 Benchmark：

| Benchmark | 主要評測內容 |
|---|---|
| LongBench v2 | 真實長上下文任務、深度理解與推理 |
| RULER | 長上下文資訊檢索與處理能力 |
| LongBench-Write | 超長篇生成能力 |
| MMLongBench-Doc | 含圖表、圖片與複雜版面的長 PDF 理解 |
| M-LongDoc | 超長多模態文件的開放式問題回答 |
| MMDocIR | 多模態文件的頁面及版面元素檢索 |
| FactRBench | 長篇回答的事實精確率與完整度 |
| GaRAGe | RAG 回答的來源依據與事實對應 |

相關論文與 Benchmark：<Cite refs={["turn0search2","turn0search3","turn3search2","turn3search3","turn3search10","turn3search0","turn3search13"]}/>

**最重要的評測原則：不要只測 Needle-in-a-Haystack。**

能從 100 萬 Token 中找到一個隱藏字串，並不代表模型能找出整份文件的所有重要證據、比較相互矛盾的說法，或正確產生數萬字報告。

如果研究目標是長文件閱讀與撰寫，評測必須同時涵蓋 Information Retrieval、Global Coverage、Reasoning 和 Generation。



---

## 🤖 Assistant 回應 (Turn 37)

## 十一、把研究方向組合成完整系統

如果要設計一套能夠閱讀數百萬 Token，並撰寫數萬字技術報告的 LLM 系統，可以將研究拆成離線資料處理與線上任務執行兩個部分。

<box border radius="xl" padding={3} gap={2}>
  <badge color="info">Offline Pipeline</badge>
  <title size="lg">文件匯入與知識建構</title>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">01 — Parsing</text>
    <text size="sm">PDF / OCR / Layout / Table / Figure Extraction</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">02 — Structure & Chunking</text>
    <text size="sm">Document Tree + Semantic Chunk + Parent–Child Index</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">03 — Knowledge Extraction</text>
    <text size="sm">Entity / Relation / Fact / Claim / Evidence</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <grid columns={3} gap={2}>
    <grid-item border radius="md" padding={2} align="center">
      <text weight="medium" size="sm">Text Store</text>
      <text color="secondary" size="xs">原文與引用</text>
    </grid-item>
    <grid-item border radius="md" padding={2} align="center">
      <text weight="medium" size="sm">Vector / Tree</text>
      <text color="secondary" size="xs">語意與層級</text>
    </grid-item>
    <grid-item border radius="md" padding={2} align="center">
      <text weight="medium" size="sm">Graph Store</text>
      <text color="secondary" size="xs">實體與關係</text>
    </grid-item>
  </grid>
</box>

<box border radius="xl" padding={3} gap={2}>
  <badge color="success">Online Pipeline</badge>
  <title size="lg">查詢、理解與文件撰寫</title>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">04 — Task Planning</text>
    <text size="sm">問題分類、子任務分解、寫作大綱與資訊需求</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">05 — Adaptive Retrieval</text>
    <text size="sm">Dense / Sparse / Graph / Global / Multimodal Search</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">06 — Reranking & Compression</text>
    <text size="sm">相關性排序、證據完整性、動態 Token Budget</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">07 — Reasoning & Evidence Synthesis</text>
    <text size="sm">跨章節整合、矛盾辨識、推理與來源追蹤</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">08 — Long-form Writing</text>
    <text size="sm">逐章生成、Document Memory、全局一致性</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box background="surface-secondary" radius="md" padding={2}>
    <text weight="medium">09 — Verification & Revision</text>
    <text size="sm">逐項核對主張與來源；不足則重新檢索與修訂</text>
  </box>
  <box align="center"><icon name="arrow-down" color="secondary"/></box>
  <box border radius="md" padding={2} align="center">
    **10 — Final Report**
    <text size="sm" color="secondary">具有完整結構、證據及交叉引用的長文件</text>
  </box>
  <caption>此流程是一種可供研究與實作的架構，不代表每個階段都需要不同模型，也不代表所有文件都需要建立完整知識圖譜。</caption>
</box>

## 十二、如果要選擇一個有研究價值的題目，可以怎麼切？

若研究重點是「超長文件理解 + RAG + 長篇報告生成」，以下六種題目各自對應不同的核心問題。

<box gap={3}>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 A：全局理解</badge>
    <title>Global-aware Hierarchical RAG</title>
    <text color="secondary" size="sm">核心問題：如何在不把全部原文放入 Context Window 的情況下，回答需要涵蓋整份文件的問題？</text>
    **研究組合：** Hierarchical Retrieval + Query Classification + Global Summarization + Evidence Coverage。

    實驗可以比較 Flat RAG、RAPTOR、GraphRAG，以及動態切換局部與全局檢索的混合架構。

    關鍵指標：全局資訊覆蓋率、答案正確率、Token Cost。
  </box>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 B：壓縮效率</badge>
    <title>Query-aware Evidence-preserving Compression</title>
    <text color="secondary" size="sm">核心問題：能否減少輸入 Token，同時保留跨章節推理所需的全部關鍵證據？</text>
    **研究組合：** Reranking + Sentence-level Compression + Atomic Fact Extraction + Adaptive Token Allocation。

    可研究在不同壓縮比例下，保留條件、否定、數字與跨文件關係的能力。

    關鍵指標：Compression Ratio、Answer Accuracy、Evidence Recall、Latency。
  </box>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 C：知識表示</badge>
    <title>Structure-aware / Proposition-based RAG</title>
    <text color="secondary" size="sm">核心問題：文件中的表格、規格條件、例外與交叉引用，應如何表示才能避免檢索與生成時失真？</text>
    **研究組合：** Structure-aware Parsing + Atomic Proposition + Condition Extraction + Hybrid Retrieval。

    實驗可選擇工程規格書、技術手冊或學術論文，比較一般 Chunk 與結構化知識表示。

    關鍵指標：Numerical Accuracy、Condition Recall、Faithfulness、Retrieval Recall。
  </box>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 D：持續記憶</badge>
    <title>Version-aware Document Memory</title>
    <text color="secondary" size="sm">核心問題：當文件內容持續修改時，如何維護正確、可更新、可追溯的長期記憶？</text>
    **研究組合：** Semantic Memory + Temporal Knowledge Graph + Conflict Detection + Incremental Index Update。

    可比較每次重新建立索引、只新增記憶，以及版本感知的記憶更新策略。

    關鍵指標：Knowledge Freshness、Conflict Rate、Update Cost、Answer Accuracy。
  </box>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 E：長篇撰寫</badge>
    <title>Evidence-grounded Long-form Document Generation</title>
    <text color="secondary" size="sm">核心問題：如何將大量來源知識轉換為數萬字、跨章節一致且引用可驗證的文件？</text>
    **研究組合：** Hierarchical Planning + Evidence Store + Iterative Writing + Document Memory + Global Revision。

    可比較 One-shot Generation、固定大綱逐章生成，以及具備動態檢索與驗證的多階段寫作架構。

    關鍵指標：Factual Precision、Content Coverage、Global Coherence、Citation Accuracy。
  </box>
  <box border radius="lg" padding={3} gap={2}>
    <badge color="info">方向 F：智慧化資源分配</badge>
    <title>Adaptive Context Budgeting</title>
    <text color="secondary" size="sm">核心問題：系統何時應使用 Full Context、何時應壓縮、何時應檢索，以及各步驟應分配多少 Token？</text>
    **研究組合：** Query Complexity Estimation + Adaptive Retrieval + Context Compression + Budget Allocation + Sufficiency Estimation。

    可以把資訊覆蓋率與模型正確率當作品質約束，研究如何降低端到端成本。

    關鍵指標：Cost per Correct Answer、Peak VRAM、Latency、Answer Quality。
  </box>
</box>

這六種並不是已經定義好的論文名稱，而是根據上述文獻整理出來、可以進一步發展成研究問題的方向。要成立為研究貢獻，還需要明確的新方法、基準比較、消融實驗與失敗情境分析。

### 一個可實作的起始實驗

假設手上有一個支援 128K Context 的開源模型，資料集共有 1M Token。

可以建立四個對照組：

| 系統 | 處理方式 |
|---|---|
| Baseline A | 將全文切成數個 128K 視窗，分別理解後彙整 |
| Baseline B | BM25 + Dense Retrieval + Reranking |
| Baseline C | Hierarchical RAG + 文件摘要樹 |
| Proposed | Hybrid Retrieval + 動態證據選取 + Context Compression + Sufficiency Verification |

對所有系統使用相同的測試問題、基礎生成模型，以及可比較的資源預算。

問題應刻意包含局部資訊、跨章節推理、整份文件的資訊聚合、數值與條件判斷，以及文件中根本沒有答案的情況。

若還要評估長篇撰寫，就讓四個系統產生相同篇幅與題目的報告，再比較事實正確率、內容涵蓋率、引用可追溯性和跨章節一致性。

這樣才能回答真正的研究問題：新方法是否在相同資源限制下，改善了長文件理解與撰寫的品質，而不是只增加更多模組和 LLM 呼叫。



---

## 🤖 Assistant 回應 (Turn 38)

## 十三、2026 年研究版圖的核心問題

綜合這些研究，可以把長文件處理的技術發展理解為三個層次：

<box gap={2}>
  <row align="start" gap={2}>
    <badge color="secondary">第一層</badge>
    <box flex="1">
      **提高模型可處理的資訊量**

      Long Context、Efficient Attention、Compression、KV Cache Optimization。
    </box>
  </row>
  <divider color="subtle"/>
  <row align="start" gap={2}>
    <badge color="info">第二層</badge>
    <box flex="1">
      **提高模型取得與使用資訊的能力**

      RAG、Knowledge Representation、Memory、Hierarchical Reasoning、Adaptive Context Management。
    </box>
  </row>
  <divider color="subtle"/>
  <row align="start" gap={2}>
    <badge color="success">第三層</badge>
    <box flex="1">
      **讓模型完成有全局約束的長期任務**

      Long-form Generation、Agentic Workflow、Evidence Verification、Document-level Revision。
    </box>
  </row>
</box>

目前這些方向並未收斂成單一架構。2025 年的 Context Engineering Survey 已明確將 Context Retrieval、Processing、Management、RAG、Memory 與 Agent 系統放在同一個研究框架下，並指出長篇生成與長上下文理解之間仍存在重要的能力落差。<Cite refs={["turn0search26"]}/>

對超長文件來說，最根本的問題也不是如何把所有 Token 永久塞進模型。

而是：**如何讓模型在任何一個工作階段，都能取得當下需要的資訊，同時維持對整份文件的全局認知，並在資訊不足時可靠地回到原始來源。**

以下是將上述研究方向整理在一起的心智圖。圖中主要呈現研究領域間的階層關係；詳細的子技術、代表論文與實驗方法則以本文的分類為準。



---

## 👤 使用者提問 (Turn 45)

請徹底的研究目前做這件事請有哪些這些領域，而這些領域具體有哪些研究方向 以及做了什麼?做到什麼程度 誰做的 還能怎麼樣

@深度研究 

---

## 🤖 Assistant 回應 (Turn 56)

深度研究已開始處理這個題目。

它會先建立研究計畫，再針對 **Long Context、Compression、RAG、Knowledge Representation、Memory、Hierarchical Reasoning、Long-form Generation、Agentic Workflow、Verification、Evaluation/Systems** 等方向進行系統性研究，並補充你未列出的相關研究領域。

最終完整研究報告會由「深度研究」介面更新。

---

## 👤 使用者提問 (Turn 57)

一些參考資料

---

## 🤖 Assistant 回應 (Turn 69)

已把你補充的參考資料加入同一個深度研究任務。 *(參考資料)* 

Deep Research 會更新原本的研究計畫，並特別對其中提到的論文、年份、方法與 2026 新工作回查原始來源，避免把參考資料中尚未核實的內容直接當成事實。

---

## 👤 使用者提問 (Turn 71)

請更徹底的研究目前做這件事請有哪些這些領域，而這些領域具體有哪些研究方向 以及做了什麼?做到什麼程度 誰做的 還能怎麼樣 並結合你上述研究過的內容
@深度研究   

---

## 🤖 Assistant 回應 (Turn 82)

已把這次要求加入同一個 Deep Research session，並大幅擴張研究範圍與深度。

Deep Research 會更新原本的研究計畫，結合你先前提供的參考資料與前一輪研究，繼續做原始論文、官方文件與 2023–2026 新工作的交叉核實。最終會形成一份偏 **Survey + Research Agenda + Reference Architecture + Novelty Landscape** 的完整技術研究報告。

---

If you want, I can:

- 繼續展開RAG剩餘細分階段
- 深入解析Compression子領域應用場景
- 詳細說明Long ContextChapter中Attention優化方法

---
