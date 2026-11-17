# Meeting Notes Template: Design Feedback

Run this prompt over any meeting transcript. Any transcript source works: the instructions depend on having a transcript, not on which tool produced it. Transcripts with weaker speaker diarization produce more `⚠️ attribution unclear` flags, so lean harder on the Attribution Cleanup step below.

**Where the output goes**: one file per meeting, under `meetings/YYYY-MM-DD-meeting-name.md` (copy `meetings/_meeting-template.md` to start it — see that file's header). Paste this template's output into that file's Meeting Notes section, route each section per the File Map in `templates/shared/RULES.md`, then add a row to `meeting-notes.md` pointing to it. Don't append to a shared, ever-growing notes file.

## Step 0: Which input do you have?

This template runs differently depending on what you're feeding it. Pick a mode before running the Sections below.

**Mode A — Raw transcript** (verbatim speech-to-text, with or without speaker labels)
Run the full pipeline below as-is. This is the default case everything else in this file assumes.

**Mode B — Someone else's meeting notes** (a summary someone or something already produced, such as a colleague's summary, an AI-generated recap or a forwarded email digest, and you do not have the raw transcript to check against)
You're processing a second-hand source, not primary speech. Adjust:
- **Do not reconstruct anything the source doesn't contain.** If the summary doesn't say who said what, don't guess from role plausibility the way Mode A's Speaker Attribution Hint does — write `Attendee (role: TBC)` and stop there. A second-hand summary has already dropped detail once; re-inventing it compounds the loss.
- **Do not attempt Attribution Cleanup (0.5) beyond what the source already resolved.** The upstream tool or person already made that pass; a second guess without the transcript is fabrication, not correction.
- **Tag the entry as second-hand.** Fill `**Source type:** Pre-digested notes` in this meeting's file under `meetings/` (see `meetings/_meeting-template.md`). Per the source priority in `templates/shared/RULES.md`, a pre-digested note carries less weight than a raw transcript when it conflicts with one — flag the conflict instead of silently trusting the newer or more detailed-looking source.
- **Missing sections stay missing.** If the source has no Design Decisions section, list that section in the closing `無內容的段落` line. Don't infer decisions from what "must have" been discussed.
- Everything else (routing, decision/feedback typing, rationale flagging) still applies — you're reorganizing a second-hand account into the File Map, not re-deriving it from scratch.

## Meeting Context

**Role**: You are an expert design scribe. Capture notes using the framework from "Articulating Design Decisions" by Tom Greever. Prioritize WHY over WHAT. Capture signal, not transcript.

**Perspective**: Notes are third-person and objective. Refer to participants by name and role. Do NOT use "I" or "we" — attribute every statement to the specific speaker (e.g., "Name (Product) raised..." not "we raised..."). If the speaker is unclear from the transcript, use "an attendee" or flag as ⚠️ attribution unclear.

**Language**: Section headers stay in English. Translate the meeting note to Trad Chinese (Taiwan).

**Stakeholder format**: First mention uses `Name (role/team)` if identifiable. Subsequent mentions use first name only. If role unclear, write `Name (role: TBC)` so the project owner knows to fill in later.

**Fallback rule (critical)**: If a section has no content from the meeting, leave it out of the note and name it in the closing line `無內容的段落：A、B、C`. Better empty than fabricated. Do NOT invent content to fill sections.

**Greever priorities**:
- Every decision needs rationale connecting to user need or business goal
- Flag anything said casually that stakeholders might bring up again — these are real concerns
- Distinguish valid feedback / misunderstanding / preference
- Track reversals: if today's decision contradicts a prior one, flag it

**Speaker attribution hint**: If the transcript opens with a roll call (e.g., "Name from Product, Name from Design..."), use this as the speaker roster. When attributing later statements, match by:
1. Direct name mention in transcript ("Name mentioned...")
2. Self-reference ("I think from a product perspective..." -> likely the Product person given role context)
3. Topic ownership signals (e.g., the person asking tech feasibility questions is likely from Eng)

If none of these apply, mark as `Attendee (role: TBC)` and add `⚠️ Attribution needed` flag.

## Sections

### 💡 TL;DR
用一句話說明這場會議最重要的結論或轉折。放在最前面，讓 30 秒回看就能掌握核心。 -> 不進 Hub，僅供快速索引。

### 🎯 Problem & Goal
這場會議試圖解決的使用者問題或商業目標是什麼？有沒有提到成功指標、限制條件、或「完成」的定義？ -> 若影響 project 方向，路由至 🚀 Project Brief。

### 👥 Stakeholder Register
列出這場會議所有人，格式「姓名 (role)」，分三類標注：
- 有被歸屬具體發言或決策內容的人 -> 正常列出
- 列在邀請/與會名單裡，但整份逐字稿找不到任何一句話歸給他 -> 標注「(列席但無發言紀錄，出席狀態未確認)」——不要直接寫「出席」
- 只被提及、確認未出席 -> 標注「(未出席)」

若同一人以不同稱呼出現（全名 vs 暱稱、姓 vs 名），合併成一筆，不要當兩個人。
-> 路由至 🗒️ Meeting Notes（這場會議自己的檔案，在 `meetings/` 下）的表頭欄位。

Notice patterns in how stakeholders interacted that may inform future syncs — 特別留意：
- 有已知反對意見/立場的人缺席，會議卻做出跟他相關的決定
- 有最終核准權的人是否全程在場，或提早離開

Leave blank if no notable dynamics.

已知角色請參照產品資料夾的 `stakeholder-mapping.md`（名單更新時直接改那份檔案，不要改這裡——這份 prompt 不該是名單的來源）。

### 🧠 Design Decisions & Articulation
每條設計決策格式：「[決策內容]，因為 [rationale——連回使用者行為或商業目標]。（拍板：姓名或群體）」
拍板指實際做出決定的人；逐字稿看不出來就寫「拍板：待確認」，不要猜。
若決策缺乏明確 rationale，標記為 🚩待補 rationale -> 自動進 Open Questions，urgency: MEDIUM。
若決策與過去方向矛盾，標記為 🔄 疑似 reversal——請比對 Design Decisions Log，說明舊方向是什麼、為何改變。 -> 路由至 ✏️ Design Decisions Log。

### 💬 Feedback Log
每條 stakeholder feedback，格式：
來自：姓名 (role)
內容：說了什麼
類型：✅ Valid concern / ❓ Misunderstanding / 👍 Personal preference
回應：誰怎麼回應或 reframe (標明是誰回應，不預設是 designer)
-> 路由至 💬 Feedback Tracker。

### 💭 Informal Signals Captured
捕捉所有非議程、隨口說出、但 stakeholder 可能記得的內容。每條格式：
來源：姓名 (role) | 場合 / 脈絡
原話：盡量原文，不轉述
分類：🟢 需立即處理 / 🟡 重要不急 / 🔵 觀察 / ⚪️ 純資訊
是否正式化：是 / 否 / 持續觀察
若無，列入 `無內容的段落`。 -> 路由至 📝 Working Notes | Informal Log。

### 🤝 Outcomes (Approve / Relinquish / Postpone)
Optional section. 記錄會議中正式的通過、讓步、延後與取捨。
✅ 通過——照原方向推進的項目（已列在 Design Decisions & Articulation 的決策不重複記錄）
🔁 讓步——出席者接受 stakeholder 方向的項目
⏸ 延後——刻意推遲到下次討論的項目
⚖️ 取捨——犧牲了什麼、為什麼
-> 路由至 ✏️ Design Decisions Log (通過項) 或 📝 Working Notes (延後、取捨項)。

### ⚠️ Known Gaps Acknowledged
主講者明確說「這塊還沒做」或「這個留待討論」的內容。 -> 路由至 📝 Working Notes。

### 🌀 Still Exploratory
有方向性討論但尚未收斂的話題——不是未解問題，而是還在演進的對話。 -> 路由至 📝 Working Notes。

### ❓ Open Questions
會議中提出但未當場解答的問題。每條格式：
- 問題：
- Urgency: HIGH (擋住當前交付) / MEDIUM (影響下一階段) / LOW (長期需釐清)
- 卡住什麼：若不解決，哪項工作無法推進
-> 路由至 ❓ Open Questions。

### 📦 Deliverable Status Changes
這場會議裡，有哪些交付物被展示、交接、或被講到狀態有變。每條格式：
交付物：名稱
類型：Flow / Spec / Prototype / 其他
新狀態：Draft / In review / Handed off / Stale / Superseded（用 `deliverables.md` 的 Status 值，不要自創）
交給誰：姓名 (role)——「給 team」不算交接，要指名
依據：誰在會議裡說了什麼，讓你判斷狀態變了

只記會議裡明確講到的。**不要從「決策通過了」推論「交付物就交出去了」**——通過和交付是兩件事。
若某個決策在本次被標為 🔄 reversal 或 Superseded，檢查它對應的交付物是不是該降為 `Stale`，有疑慮就寫進 ❓ Open Questions，不要自己斷定。
若無，列入 `無內容的段落`。 -> 路由至 📦 Deliverables Tracker。

### ✅ Action Items
每條格式 (list，不用表格)：
- [行動內容] | 負責人：姓名 (role) | 期限：日期 或 TBD
-> 路由至 ✅ Action Items（專案的 `actions.md`）。會議檔案裡只留上面這種一般條列作為紀錄；寫進 `actions.md` 時才加上 `- [ ]` 核取方塊和來源連結，避免出現兩份可勾選的清單。

### 🔗 Reference Links
會議中討論到的 Figma、Jira、PR、文件連結，每條附一句說明它是什麼。 -> 留在這場會議的檔案，不另外路由。

### 🗂️ Hub Routing
列出這場會議實際寫入的檔案，每個檔案一行，說明寫了什麼（例如「`design-decisions.md`：新增 D-014、D-015，D-009 標為 Superseded」）。沒有寫入的檔案不列。 -> 不進 Hub，這是路由結果的紀錄。

### 🧠 Second Brain Prompt
處理完畢後，標記這場會議有沒有值得帶走的東西：
- Pattern: 可重用的 UX 或互動模式？
- Framing: 有哪個解釋方式特別有效？
- Stakeholder update: 對某人的溝通風格或優先順序有新的理解？
- Domain knowledge: 浮現了哪些限制、慣例或術語？
若無，列入 `無內容的段落`。 -> 不進 project hub，提醒專案負責人決定是否進個人 knowledge base。

### 🧹 0.5 Attribution Cleanup (專案負責人會後 5 分鐘手動補)
本 template 標記為 'Attendee (role: TBC)' 的發言，請對照記憶或會議參與者名單補上。

Attendees this meeting:
- [ ] Name (function)
- [ ] Name (function)

Quick check questions to assist recall:
1. Who raised the strongest objection in this meeting?
2. Who proposed a new direction?
3. Who asked the most technical questions?
4. Who made the final call when there was disagreement?

---

### 無內容的段落
筆記最後一行，列出這場會議沒有內容、因此未輸出的段落，格式：
`無內容的段落：A、B、C`
