---
title: "Domain 04: Chunking 策略與知識擷取 (Proposition-level, Semantic Boundary, Cross-chunk)"
tags:
  - "domain/chunking-knowledge"
  - research-domain
---

# Domain 04: Chunking 策略與知識擷取 (Proposition-level, Semantic Boundary, Cross-chunk)

> [!ABSTRACT] 核心問題意識 (Core Problem Statement)
> **文件切塊（Chunking）絕非單純的字數切片，而是最關鍵的『知識表示（Knowledge Representation）』工程。如何將非結構化長文本解構為語意自足、無歧義的知識單元？**

---

### 一、核心問題意識：Chunking 是知識表示問題
長文本處理的失敗，超過一半起源於最前端的切塊錯誤。固定字數切塊（如 512 tokens + 10% overlap）存在以下本質缺陷：
1. **語意割裂**：一個完整的句子或邏輯證明被攔腰斬斷在兩個 Chunk 之中。
2. **代名詞懸空（Pronoun Ambiguity）**：Chunk 內大量出現『他』、『該公司』、『這項政策』，脫離前文後在向量空間中成為無法定位的漂浮向量。
3. **條件與例外遺失**：主句在 Chunk A，但前提條件『除非在以下情況下...』落在 Chunk B，導致檢索檢索出完全相反的事實。

---

### 二、知識單元抽象層次階梯

```text
文件 (Document)
 │
 ├─ 原始段落 (Raw Passage) ─── 包含大量冗餘、格式符號與口語修飾
 │
 ├─ 語義段落 (Semantic Chunk) ── 依段落結構、標題 Markdown 層次切分
 │
 ├─ 命題 (Proposition) ─────── 最小、原子級、語義自足的事實陳述 (Dense X)
 │
 ├─ 實體與關係 (Entity & Triple) ─ (主詞, 謂詞, 受詞) 三元組，如 (Apple, acquires, Beats)
 │
 └─ 主張與證據鏈 (Claim & Evidence) ─ 具備時空、置信度與支持文檔定位的命題
```

---

### 三、命題級切塊：Dense X (Proposition Retrieval)
- **代表作**：[[Chen2023 - Dense X Proposition Retrieval|Dense X (Chen et al., EMNLP 2024)]]。
- **核心定義**：將長文切分為一個個『Proposition（命題）』。每個命題必須具備：
  1. 包含一個獨立的原生事實；
  2. 最小化（不可再分）；
  3. 語意完全自包含（將所有代名詞替換為明確全稱實體，補齊所屬時間與背景條件）。
- **範例**：
  - *原文*：「愛因斯坦於 1879 年出生於德國烏爾姆，翌年隨家人遷居慕尼黑，在那裡他完成了早期的中學學業。」
  - *解構命題 1*：「愛因斯坦於 1879 年出生在德國烏爾姆。」
  - *解構命題 2*：「愛因斯坦於 1880 年隨同其家人遷居至慕尼黑。」
  - *解構命題 3*：「愛因斯坦在德國慕尼黑完成了早期的中學學業。」

---

### 四、三元組（Triple）的局限與跨塊抽取難題

#### 1. 為什麼純 Triple (S, P, O) 不是最理想的知識表示？
- 傳統知識圖譜習慣使用三元組 `(Subject, Predicate, Object)`。
- **致命缺陷**：三元組徹底抹殺了**語義脈絡**。例如：
  - 法律條文：「在未滿 18 歲且未獲法定監護人同意之情形下，該契約視為無效。」
  - 若強行抽取三元組 `(契約, 效力, 無效)`，完全丟失了『未滿 18 歲』與『未獲監護人同意』這兩個關鍵先決條件。
  - 因此，**命題圖（Proposition Graph）** 或 **富屬性超圖（Hypergraph）** 遠比純三元組更適合長文法律、金融、醫療文件。

#### 2. Cross-Chunk 知識擷取的挑戰
- 許多核心知識分散在不同章節：
  - 第一章提到：「專案代號 Titan 於 2021 年立項。」
  - 第十章提到：「該代號團隊於 2024 年初遭到全面裁撤。」
- 若各 Chunk 獨立處理，系統永遠無法抽取出『Titan 專案生命週期為 2021-2024』這一高價值宏觀事實。
- **前沿解法**：兩階段抽取 —— 第一階段在各局部 Chunk 抽取實體與局部事實；第二階段啟動 Cross-Chunk 實體對齊與矛盾消解聚類，將分散線索合併為全局事實節點。

---

## 相關導覽與文獻快速跳轉
- **回主目錄**：[[00 - 導覽與心智圖 (Navigation & MOC)/Home (主目錄與知識庫導覽)|主目錄與知識庫導覽]]
- **全景心智圖**：[[00 - 導覽與心智圖 (Navigation & MOC)/LLM 超長文件處理心智圖 (MOC)|超長文件處理研究方向心智圖]]
- **深度研究報告**：[[01 - 深度研究報告 (Deep Research Reports)/01 - LLM 超長文件閱讀與撰寫技術全景 (完整深度報告)|技術全景深度報告]]
- **權衡分析**：[[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術成熟度與 Pareto 權衡分析]]
