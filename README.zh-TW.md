# Crit-Ready

[English](README.md) | **繁體中文**

**讓設計師在 Design Review 裡，永遠說得出「為什麼」。**

Crit-Ready 是一套專為 B2B UX 設計師與 AI Agent (Claude Code 與 Codex) 打造的專案知識模板與決策軌跡系統。它不是給人讀的傳統文件，而是**給 AI 檢索的第二大腦**。

---

## 💡 解決的核心痛點

1. **決策失憶**：Slack 或會議口頭決定後，找不到脈絡，導致重複討論。
2. **來源打架**：Jira、Figma 留言、會議紀錄衝突時，不再需要到處問人。
3. **跨專案知識斷層**：把單次專案的經驗，轉化為團隊可複用的設計模式。

---

## ⚙️ 安裝設定

Crit-Ready 有兩個部分，兩者要放在同一個資料夾，也就是你的 **vault**（Obsidian vault，或任何放 markdown 筆記的資料夾）：

- `templates/`：檔案模板與共用規則。含有 `templates/` 的那個資料夾就是 vault 根目錄。
- `crit-ready` skill：agent 照著做的指令，放在 `.agents/skills/crit-ready/`。

### 方法 A：開一個新的 vault

直接 clone 這個 repo 當作你的 vault，用 Obsidian 開這個資料夾，並在裡面啟動 agent。

```
git clone https://github.com/falinwang/crit-ready.git my-vault
cd my-vault
```

所有東西都已經就位。`.claude/skills` 是指向 `.agents/skills` 的連結，所以 Claude Code 和 Codex 都找得到 skill。

### 方法 B：加進你已經在用的 vault

把三樣東西複製到 vault 根目錄：

```
cp -R crit-ready/templates          my-vault/
mkdir -p my-vault/.agents/skills
cp -R crit-ready/.agents/skills/crit-ready crit-ready/.agents/skills/greever  my-vault/.agents/skills/
```

如果用 Claude Code，再把它的 skills 資料夾連到同一個地方：

```
mkdir -p my-vault/.claude
ln -s ../.agents/skills my-vault/.claude/skills
```

選擇性：如果你的 vault 已經有自己的資料夾配置（例如 PARA），在 vault 的 `AGENTS.md` 寫明專案和產品放在哪裡，指令會照著做。

### 各 agent 從哪裡讀 skill

| Agent | 放在 vault 裡 | 電腦上所有資料夾都能用 | 執行指令 |
| :--- | :--- | :--- | :--- |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/crit-ready minutes` |
| Codex | `.agents/skills/` | `~/.agents/skills/` | `$crit-ready minutes` |

skill 也可以裝在個人資料夾而不放在 vault 裡，但 vault 仍然需要 `templates/`，因為 skill 是靠它找到 vault 根目錄和規則。

### 更新

把新的 `templates/` 和 `.agents/skills/crit-ready/` 拉下來或複製過去覆蓋舊的即可。這只會換掉模板和指令；你的專案、`pattern-library.md` 和 `TODAY.md` 是另外的檔案，不會被動到。舊版建立的專案照常可用，想轉成新結構時再執行 `/crit-ready migrate`。

---

## 🚀 內建 AI 指令 (Skills)

所有指令都在同一個 `crit-ready` skill 底下（`.agents/skills/crit-ready/`），所以 `/crit-ready` 是真正的斜線指令，後面接子指令：

### 1. `/crit-ready init [產品]/[專案]` (Project Scaffolding)
建立新專案時的自動化腳本。同一個產品的多個階段（phase 1、2、3）屬於同一個產品，共用產品層級的知識。當你輸入此指令，Agent 會：
- 找到或建立產品（`PRODUCT.md` 與 `stakeholder-mapping.md`），再從 `templates/design-project/` 複製專案資料夾結構。資料夾放哪裡依你 vault 自己的慣例，沒有慣例才預設把專案放在產品資料夾底下。
- **延續上一階段**：若產品已有前一個專案，列出可以帶過來的項目（未解問題、延後項目、未完成行動、未回應的有效回饋），由你挑選；也可以把前一階段仍有效的決策升級為產品的長期決策。
- **主動防呆**：掃描跨專案模式庫 (`pattern-library.md`)，有相關前例就提前提示你，沒有就明說「no matching precedent found」。
- **Kickoff 三問**：成功長怎樣？怎麼衡量？誰負責衡量？Agent 只根據你已提供的資料起草答案，還沒有答案可以先寫 `TBD (to settle at the Kickoff meeting)`。

### 2. `/crit-ready minutes` (Design Knowledge Coordinator)
丟入會議逐字稿（或別人整理好的摘要），AI 不只是產出摘要，而是把內容歸檔進 Hub：
- 筆記寫進該場會議自己的檔案（若已用 `/crit-ready prep` 建立就沿用），並依 File Map 分流到決策、待解問題、回饋、行動項目等檔案。
- **決策動機**：每條決策都帶 `因為 [rationale]` 與拍板者；沒有 rationale 的決策標為 `Pending` 並開一條待解問題。
- **行動項目**進入專案的 `actions.md`，成為唯一可勾選的清單。
- 回覆一段可直接貼到 Slack 的摘要，並列出需要你處理的事（歸屬確認、疑似推翻、Pending 決策、與產品長期決策的衝突）。

### 3. `/crit-ready sync [決策內容]` (Low-friction Decision Sync)
在 Slack 或 Figma 上的零碎討論，無痛轉化為正式決策：
- 自動比對並取代 `design-decisions.md` 中舊有的衝突決策（以決策 ID 標示，如 `Superseded (→ D-015)`）。
- 關閉 `open-questions.md` 中對應的待辦問題，後續任務寫進 `actions.md`。
- 產生一句確認語句，讓你直接貼回 Slack 完成 Lock-in。

### 4. `/crit-ready promote` (Pattern Graduation)
將專案內經過實戰驗證的決策升級，有兩個去處：
- `/crit-ready promote [決策] to product`：升級為產品的長期決策，寫入 `PRODUCT.md`，之後同產品的每個專案都會被提醒。
- `/crit-ready promote [決策]. Outcome: [...]. Tags: [...]`：把包含結果 (Outcome) 的決策提煉至全域的 `pattern-library.md`，供其他產品參考。

兩者都只在你下指令時才執行，Agent 不會自動升級。

### 5. `/crit-ready prep [會議名稱/主題]` (Pre-Meeting Prep)
開會前，根據 Tom Greever《Articulating Design Decisions》哲學，從 Hub 現有資料為你準備會前文件，並建立這場會議的檔案：
- **開場定調 5 步驟**：自動從專案簡介、決策與上次會議抓取目標與上次結論，避免會議失焦。
- **兵推與預測反應**：只在需要拍板的會議（Crit、Executive Review）進行，每個預測都連回該與會者過去的回饋紀錄；沒有紀錄就直說，不憑職稱猜。
- **挑選適用的 Greever 技巧**（如 Rule of Direct Comparison、Design Advocates），而非全部套用。例行同步只給狀態摘要。

### 6. `/crit-ready today` (Daily To-Do)
掃描所有專案，產生放在 vault 根目錄的 `TODAY.md`：
- 依產品與專案分組，列出我的行動項目、我負責的 HIGH 待解問題、等待確認的 Pending 決策、未回應的有效回饋，以及只有會前準備沒有會後筆記的會議。
- `等別人` 與 `該回頭看` 兩個區塊提醒卡住的事與該複查的舊紀錄。
- `TODAY.md` 只是產生出來的檢視，真正的資料仍在各來源檔案；在 `TODAY.md` 勾選的項目，下次執行時會回寫到 `actions.md`。

### 7. `/crit-ready migrate [專案]` (Migrate an Older Project)
把舊版結構的專案轉成目前的結構，一次一個專案，只在你下指令時執行：
- 先讀完整個專案，列出每個檔案會怎麼改、哪些地方它無法自行判斷，等你同意後才動手。
- 動手前完整備份專案資料夾。
- 決策補上 ID、會議檔裡的待辦集中到 `actions.md`、名冊併入產品層；既有的列與文字一律保留，不改寫內容。

---

## 📂 核心知識架構 (Log → Link → Lock)

整個 vault 分成三個層級：**vault**（跨產品）、**product**（同一產品的所有階段）、**project**（單一階段或專案）。

三個層級是用檔案和連結定義的，不是用資料夾位置：專案是任何含有 `FOLDER-INSTRUCTIONS.md` 的資料夾，它的產品是該檔案連結到的那份 `PRODUCT.md`。所以你的 vault 可以維持原本的組織方式（例如 PARA：專案和長期資料分開放）。沒有既定慣例時，預設配置如下：

```
vault/
  templates/            shared/（規則，只存一份）、product/、design-project/、vault/（schema）
  pattern-library.md    跨產品的模式庫
  TODAY.md              每日待辦（自動產生）
  <product>/
    PRODUCT.md          長期決策、領域知識、延後項目
    stakeholder-mapping.md
    <project>/          一個階段或專案
      FOLDER-INSTRUCTIONS.md, project-brief.md, design-decisions.md, open-questions.md,
      feedback-tracker.md, working-notes.md, deliverables.md, actions.md, changelog.md,
      meeting-notes.md, meetings/
```

靜態規則（File Map、來源優先順序、ID 規則）集中在 `templates/shared/RULES.md`，不再複製進每個專案。舊版結構的專案不會被自動更動，所有指令仍可在上面運作；想轉成新結構時用 `/crit-ready migrate`。

知識沉澱遵循三階段原則：「記錄、連結、鎖定」。確保每一個設計決策都有跡可循，不再淪為無頭公案：

### 1. 📝 Log (廣泛記錄)
**目標**：捕捉所有非正式的脈絡、會議討論與原始靈感，不漏掉任何細節。
*   **`meetings/`**: 專屬會議紀錄資料夾，一場會議一個檔案，會前準備與會後筆記放在一起。透過 `/crit-ready minutes` 將混亂的逐字稿結構化並歸檔，杜絕黑盒子的 AI 摘要。
*   **`working-notes.md`**: 你的日常塗鴉牆，用來存放還沒成型的草稿與探索性想法 (Still Exploratory)。

### 2. 🔗 Link (建立連結)
**目標**：將發散的紀錄收斂成具體的決策，並強制關聯背後的 Rationale (為什麼這樣做)。
*   **`design-decisions.md`**: 決策軌跡中心，每項決策有 ID（`D-001`…）、出處與原因，解決「我們當初為什麼這樣做？」的無限迴圈。
*   **`open-questions.md`**: 追蹤卡住進度的問題，標明急迫度與卡住什麼，並指派給特定的負責人。撐過三場會議仍未解決的問題只會問你一次，之後自動擱置，不是你能決定的舊問題不會一再回來。
*   **`actions.md`**: 專案唯一的行動清單，在 Obsidian 勾選即完成。
*   **`/crit-ready sync`**: 將 Slack 或 Figma 上的對話，一鍵轉化為決策並連結回對應的檔案。

### 3. 🔒 Lock (鎖定與升級)
**目標**：確保決策被團隊認知，並在驗證成功後升級為團隊的防禦資產。
*   **`deliverables.md`**: 標示交付物的狀態 (Draft, Handed off, Stale)，避免工程師拿到過期的版本。
*   **`PRODUCT.md`**: 同一產品跨階段持續有效的決策，用 `/crit-ready promote ... to product` 鎖定。
*   **`pattern-library.md`**: 跨產品共用的設計模式庫。利用 `/crit-ready promote` 將實戰驗證過的好決策升級為全團隊的資產。

---

## 🛠️ 日常使用

1. 開新專案：`/crit-ready init 產品名稱/專案名稱`。
2. 開會前：`/crit-ready prep`，建立會議檔案與會前準備。
3. 開完會：貼上逐字稿或筆記，輸入 `/crit-ready minutes`，內容會歸檔進專案。
4. 在 Slack 或 Figma 做了決定：`/crit-ready sync`。
5. 每天開工：`/crit-ready today`，看今天要做什麼。
6. 決策經過驗證之後：`/crit-ready promote`。

在 Codex 裡把 `/crit-ready` 換成 `$crit-ready`。

> **保密會議提醒**：客戶、高層或其他機密會議，錄音前請先確認貴組織核准的工具，不要用個人或免費版 AI 筆記工具。確認其合約可選擇退出 AI 模型訓練，並符合貴組織的合規標準（SOC 2 / ISO 27001、SSO、資料所在地），而不只是看它產出的筆記好不好用。

> *致謝：決策表述方式深受 Tom Greever《Articulating Design Decisions》啟發。本專案將「當場講清楚」的理念，延伸為「事後查得到」的自動化系統。*
