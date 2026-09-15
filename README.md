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

---

## 📂 核心知識架構 (Log → Link → Lock)

專案結構設計遵循「記錄、連結、鎖定」原則，將資訊正確歸屬：

*   **`design-decisions.md`**: 決策軌跡中心，每項決策必附 Rationale (為什麼這樣做) 與來源出處。
*   **`pattern-library.md`**: 跨專案共用的設計模式庫。利用 `#promote` 將驗證過的好決策升級為團隊資產。
*   **`meetings/`**: 專屬會議紀錄資料夾，透過 `/magic-minutes` 自動結構化，杜絕黑盒子 AI 摘要。

---

## 🛠️ 如何開始

1. 將本專案 clone 至你的本地端 Workspace。
2. 開啟你的 AI Agent (如 Antigravity)。
3. 輸入 `/crit-ready init 你的專案名稱` 開始新專案。
4. 開完會後，貼上逐字稿並輸入 `/crit-ready minutes` 體驗無縫知識沉澱。

> *致謝：決策表述方式深受 Tom Greever《Articulating Design Decisions》啟發。本專案將「當場講清楚」的理念，延伸為「事後查得到」的自動化系統。*
