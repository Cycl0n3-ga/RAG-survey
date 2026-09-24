# Agent 工作守則與專案注意事項 (Project Guidelines for AI Agents)

本專案為 **LLM 超長文件處理、RAG、知識圖譜與長篇生成技術全景知識庫**。
所有在此專案中工作的 AI Agent（包含 Antigravity、Gemini、Claude、Cursor 等）**必須嚴格遵守以下 6 大核心工作守則**：

---

### 1. 分支操作原則 (Branch Policy)
- **可以直接在 `master` 分支上操作**。
- 無需強制建立額外的 feature branch，直接在 `master` 分支上進行檔案新增、編輯與維護。

### 2. 作業前置同步 (Pre-Task Sync)
- **每次作業開始前，必須先從 GitHub 遠端同步最新代碼**：
  ```bash
  git fetch origin master && git pull --rebase origin master
  ```
- 確保本機工作目錄與遠端保持完全一致，避免版本分歧或覆蓋他人/其他設備之修改。

### 3. 作業完成自動提交與推送 (Post-Task Commit & Push)
- **每當一個任務或階段性作業完成時，務必執行 `commit` 與 `push`**：
  ```bash
  git add -A
  git commit -m "type(scope): 清楚描述本次更新之實質內容"
  git push origin master
  ```
- 嚴禁作業完成後將未提交的修改留在本地，確保遠端 GitHub 儲存庫始終具備最新的研究筆記與檔案狀態。

### 4. 參考資料必須完備無缺漏 (Comprehensive & Exhaustive References)
- **引用的文獻、論文、模型、年份、會議、連結與資料來源必須嚴格精確，絕不可遺漏或簡化**。
- 若論文有 arXiv ID、ACL Anthology 連結或官方發布頁面，必須一併提供完整的永久連結。
- 新增論文時，必須同步下載原始 PDF 檔案至 `Papers/` 對應的分類子資料夾，並在 `03 - 論文庫 (Literature Notes)/` 中建立對應的結構化筆記。

### 5. 雙向交叉核對內容正確性 (Bidirectional Verification)
- **嚴格驗證事實與推論的雙向一致性**：
  - 確保筆記中的核心宣稱（Claims）與原始論文（Source Papers）的實驗數據、方法描述完全吻合，嚴禁臆測、過度推論或張冠李戴。
  - 交叉核對內部雙向連結（Obsidian Wikilinks `[[...]]`），確保筆記與 PDF 相對路徑正確無誤，無懸空斷鏈（Dangling Links）。
  - 對於有爭議的技術對比（例如 Long Context vs. RAG、SSM vs. Transformer），必須平衡呈現各自的優劣勢與適用邊界，提供完整的 Trade-offs 分析。

### 6. 存疑必問，正確性至上 (Clarify Doubts, Accuracy is Paramount)
- **若對使用者的需求、格式偏好、技術細節或資料來源存在任何懷疑或不確定性，務必主動向使用者詢問釐清，切勿自行腦補或做未經證實的假設**。
- **本專案的核心價值在於學術與工業實踐的高準確度**，正確性永遠高於單純的生成速度。

---

### 📂 目錄結構規範 (Directory Structure Convention)
- `00 - 導覽與心智圖 (Navigation & MOC)/`：存放全景 MOC、主目錄與技術選型權衡筆記。
- `01 - 深度研究報告 (Deep Research Reports)/`：存放完整深度調研報告與對話存檔。
- `02 - 研究領域專題 (Research Domains)/`：存放各細分技術領域專題分析。
- `03 - 論文庫 (Literature Notes)/`：存放各篇論文的結構化筆記。
- `Papers/`：存放依大類分類的論文 PDF 全文，檔名格式統一為 `(會議/期刊 發表年月) 論文名稱.pdf`。
