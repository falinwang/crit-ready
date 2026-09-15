# Crit-Ready

**讓設計師在 Design Review 裡，永遠說得出「為什麼」。**

Crit-Ready 是一套專為 B2B UX 設計師與 AI Agent (如 Antigravity) 打造的專案知識模板與決策軌跡系統。它不是給人讀的傳統文件，而是**給 AI 檢索的第二大腦**。

---

## 💡 解決的核心痛點

1. **決策失憶**：Slack 或會議口頭決定後，找不到脈絡，導致重複討論。
2. **來源打架**：Jira、Figma 留言、會議紀錄衝突時，不再需要到處問人。
3. **跨專案知識斷層**：把單次專案的經驗，轉化為團隊可複用的設計模式。

---

## 🚀 內建 AI 指令 (Skills)

將本專案匯入後，你可以直接透過 AI 觸發以下自動化工作流：

### 1. `/crit-ready init [專案名稱]` (Project Scaffolding)
建立新專案時的自動化腳本。當你輸入此指令，Agent 會：
- 從 `templates/` 複製完整的知識庫資料夾結構。
- **主動防呆**：掃描跨專案模式庫 (`pattern-library.md`)，若有相關前例會提前提示你。
- **強制 Kickoff 訪談**：要求你回答 3 個關鍵問題（成功長怎樣？怎麼衡量？誰負責衡量？），並自動寫入專案設定檔中對齊目標。

### 2. `/crit-ready minutes` (Design Knowledge Coordinator)
丟入混亂的會議逐字稿，AI 自動以「設計知識協調者」的角度萃取：
- **決策動機**：強制輸出 `[決策內容]...因為[rationale]` 格式
- **分層輸出**：自動切分出「Slack 快速同步版」與「Notion 知識留存版」
- **洞察提煉**：捕捉跨部門協同 Action Items 與潛藏的設計模式 (Second Brain Prompt)

### 3. `/crit-ready sync [決策內容]` (Low-friction Decision Sync)
在 Slack 或 Figma 上的零碎討論，無痛轉化為正式決策：
- 自動比對並取代 `design-decisions.md` 中舊有的衝突決策。
- 關閉 `open-questions.md` 中對應的待辦問題。
- 產生一句確認語句，讓你直接貼回 Slack 完成 Lock-in。

### 4. `/crit-ready promote [決策內容]` (Pattern Graduation)
將專案內經過實戰驗證的決策，升級為團隊的防禦機制：
- 將包含結果 (Outcome) 的成功/失敗決策，提煉至全域的 `pattern-library.md`。
- 未來團隊成員開新專案時，AI 將會自動引用這個 Pattern 避免重複踩坑。

### 5. `/crit-ready prep [會議名稱/主題]` (Pre-Meeting Prep)
開會前，根據 Tom Greever《Articulating Design Decisions》哲學自動為你準備「會前防禦劇本」：
- **開場定調 5 步驟**：自動從 `design-decisions.md` 等檔案抓取目標與上次結論，避免會議失焦。
- **兵推與預測反應**：根據與會者角色，自動套用 IDEAL 框架、Rule of Trade-Offs，並用 The Preference Ban 破解「這感覺怪怪的」等主觀批評。
- **安排暗樁 (Design Advocates)**：提醒並規劃如何會前拉攏盟友，避免你成為會議上的孤軍奮戰者 (Lonely Defender)。

---

## 📂 核心知識架構 (Log → Link → Lock)

整個專案的結構設計遵循了知識沉澱的三階段原則：「記錄、連結、鎖定」。確保每一個設計決策都有跡可循，不再淪為無頭公案：

### 1. 📝 Log (廣泛記錄)
**目標**：捕捉所有非正式的脈絡、會議討論與原始靈感，不漏掉任何細節。
*   **`meetings/`**: 專屬會議紀錄資料夾，透過 `/crit-ready minutes` 將混亂的逐字稿自動結構化，杜絕黑盒子的 AI 摘要。
*   **`working-notes.md`**: 你的日常塗鴉牆，用來存放還沒成型的草稿與探索性想法 (Still Exploratory)。

### 2. 🔗 Link (建立連結)
**目標**：將發散的紀錄收斂成具體的決策，並強制關聯背後的 Rationale (為什麼這樣做)。
*   **`design-decisions.md`**: 決策軌跡中心，每項決策都必須標明出處與原因，解決「我們當初為什麼這樣做？」的無限迴圈。
*   **`open-questions.md`**: 追蹤卡住進度的問題，並明確指派給特定的負責人。
*   **`/crit-ready sync`**: 將 Slack 或 Figma 上的對話，一鍵轉化為決策並連結回對應的檔案。

### 3. 🔒 Lock (鎖定與升級)
**目標**：確保決策被團隊認知，並在驗證成功後升級為團隊的防禦資產。
*   **`deliverables.md`**: 標示交付物的狀態 (Draft, Handed off, Stale)，避免工程師拿到過期的版本。
*   **`pattern-library.md`**: 跨專案共用的設計模式庫。當專案結束後，利用 `/crit-ready promote` 將實戰驗證過的好決策「鎖定」並升級為全團隊的資產。

---

## 🛠️ 如何開始

1. 將本專案 clone 至你的本地端 Workspace。
2. 開啟你的 AI Agent (如 Antigravity)。
3. 輸入 `/crit-ready init 你的專案名稱` 開始新專案。
4. 每次開完會：貼上逐字稿並輸入 `/crit-ready minutes` 體驗無縫知識沉澱。
5. 每天日常溝通：在 Slack 決定的事，立刻回 AI 敲 `/crit-ready sync` 記錄下來。
6. 專案結束後：有好的踩坑經驗，用 `/crit-ready promote` 升級成團隊設計模式。

> *致謝：決策表述方式深受 Tom Greever《Articulating Design Decisions》啟發。本專案將「當場講清楚」的理念，延伸為「事後查得到」的自動化系統。*
