# Design Project Agent Template

這是一個專為「AI Agent（如 Claude / Antigravity）」設計的 UX/UI 專案管理模板。

本模板的誕生來自於一個深刻的覆盤與 Paradigm Shift：**「專案文件不是給人讀的，是給 Agent 檢索的知識庫。」**
當我們把 Agent 視為專案的「設計知識總管（Design Knowledge Coordinator）」時，我們不再受限於人類的閱讀負荷，而是專注於解決**資訊歸屬錯誤**與**多來源矛盾**的問題。

---

## 💡 核心思路與機制 (The Philosophy & Rationale)

這個模板的設計深度融合了 Tom Greever《Articulating Design Decisions》的框架，並針對 AI 協作的痛點提出了以下解法：

### 1. #sync 低摩擦決策同步 (Low-Friction Decision Sync)
* **痛點**：設計師在會議、Figma 留言或 Slack 中做出的決定，往往因為「重述脈絡太花時間」而沒有記錄下來，導致決策漂移（無法 Lock in agreement）。
* **思路**：人類只負責提供差異（Diff），脈絡讓 Agent 自己找。你只需要輸入一句極簡的指令（例如：`#sync CSV 上限改為 50 by Nancy。原因：後端限制`），Agent 就會自動去比對舊決策、標記 `Superseded`、清理 Open Questions，並產出一句給 Stakeholder 的「Lock-in 確認語句」。

### 2. 嚴格歸屬與 Local Markdown 路由 (Granola Prompting)
* **痛點**：AI 會議工具（如 Granola）常憑空捏造發言人，當 Agent 將這些錯誤資訊寫入知識庫後，會產生蝴蝶效應，嚴重消耗設計師的「信任存款（Bank Account of Trust）」。
* **思路**：模板內建了高度客製化的 Granola Prompt (`granola-custom-template.md`)。它強迫 AI 執行 `Attribution Cleanup`、明確區分「確認的決策」與「隨口的提議」，並嚴格要求每條決策必須連回商業目標（Appeal to the business）。最重要的是，它規定了每一種輸出都要路由到我們專屬的 Local Markdown 表格中（如 `design-decisions.md`），而不是一個黑盒子。

### 3. 動態 PARA 架構適應 (Environment Agnostic)
* **痛點**：如果把路徑寫死成 `10-projects/`，這包模板就無法帶去其他命名習慣的 Vault 使用。
* **思路**：發揮 Agent Skill 的自然語言優勢。我們不寫死路徑，而是教 Agent「在執行 `/init` 前，先掃描根目錄，找出代表 Projects 和 Templates 的資料夾」。這讓這套工作流具備了跨 Vault 的高度適應性。

---

## 📦 內容物 (What's Included)

1. **`templates/design-project/` (專案骨架)**
   * `FOLDER-INSTRUCTIONS.md`：該專案的 Agent 大腦。內含 #sync 處理規則、Source of Truth 優先序，以及 Kickoff 必答題。
   * `design-decisions.md`：結構化的決策軌跡與 Rationale 紀錄。
   * `open-questions.md`：待釐清的問題追蹤。
   * `changelog.md`：專案異動日誌。
   * `granola-custom-template.md`：專為此系統打造的會議逐字稿 Prompt。

2. **`.agents/skills/init-project/` (Agent 啟動技能)**
   * `SKILL.md`：讓 Agent 聽懂 `/init` 指令的腳本。它會自動偵測你的 PARA 架構、建立資料夾、複製模板，並強制詢問你專案的「成功指標」。

---

## 🚀 如何使用 (How to Use)

1. 將本 Repo 中的 `templates` 與 `.agents` 資料夾內容，複製到你自己的 Obsidian 或 PARA Vault 根目錄。
2. 啟動你的 Agent（例如 Claude Code 或 Antigravity）。
3. 在對話框輸入：
   ```text
   /init work-你的專案名稱
   ```
4. Agent 會自動幫你架構好一切，並反問你專案的衡量指標。回答完畢後，即可開始工作！
