# Pre-Meeting Prep

`meeting-notes-template.md` 處理會後——把逐字稿整理進 Hub。這份檔案處理會前——會議開始前，你該準備哪份文件，才能讓那場會議值得開。

**注意：** 下面六種會議類型的 emoji 只是標題裝飾，不是 routing name。File Map（`FOLDER-INSTRUCTIONS.md`）裡那套 emoji + 名稱才是路由用的，兩套刻意不重疊——新增會議類型時，別挑已經被 File Map 用掉的 emoji。

**依據：** Tom Greever《Articulating Design Decisions》沒有給「會議類型清單」，給的是跨會議通用的技巧（Setting the Context、IDEAL Framework、Bank Account of Trust）。這份文件把那些技巧套進設計師實際會遇到的幾種會議類型，並指向 Hub 裡已經在維護的檔案——不重複建立新的資料結構。

**怎麼用：** 開會前，找到對應的會議類型，照「會前文件」欄位準備內容，寫進這場會議自己的檔案（`meetings/YYYY-MM-DD-meeting-name.md`，見 `meetings/_meeting-template.md` 的 Pre-Meeting Prep 區塊）——不要留在這份指南裡累積。這份文件本身是不隨專案演進的參考手冊，六種會議類型的做法都在這裡查，但每一場會議實際準備出來的內容屬於那場會議自己的檔案。大部分欄位是把 Hub 既有檔案裡的東西挑出來重組，不是從零生成。

---

## 🌱 Kickoff Meeting

**目的：** 對齊專案要解決的問題、範疇、成功指標，是整個專案唯一一次「定義問題」的會議。
**時機：** 專案啟動時，通常只有一次（重大改組例外）。

**會前文件：Project Brief Draft**
- 從 `FOLDER-INSTRUCTIONS.md` Layer 4 的三個 Kickoff 問題（成功長怎樣／怎麼衡量／誰負責衡量）草擬答案
- 對照 `project-brief.md` 的 Problem / Who It Affects / Roles / Constraints / In-Out of Scope / Timeline 欄位，能填多少先填多少
- 沒有答案的欄位留白，不要用會議前的猜測補上——那是會議本身要解決的事

**依據：** Ch03 *Design the Meeting* — Setting the Context 的第一步就是「說出已對齊的專案目標」；Kickoff 就是那個目標第一次被說出來的場合。

---

## 🔍 Design Review / Crit

**目的：** 拿設計方案換取具體、可行動的回饋，不是換取「喜不喜歡」。
**時機：** 每個設計階段的自然斷點——wireframe 定案前、visual 定案前、交付前。

**會前文件：Review Prep Brief**
- 重新陳述本階段目標（Setting the Context 的開場）
- 從 `design-decisions.md` 抓上一場會議定案的項目，列成「上次我們同意了什麼」
- 明確寫「這次要什麼回饋／不要什麼回饋」（例如：要 flow 是否合理，不要顏色深淺）
- 準備至少一個替代方案一起展示（Rule of Direct Comparison）——不要只帶單一版本進場

**依據：** Ch03 Setting the Context 全套流程；Cheatsheet Rule of Direct Comparison（「若 stakeholder 堅持自己的想法比較好，絕不能單獨呈現他的想法，永遠並排比較」）。

---

## 👑 Executive / Stakeholder Alignment Review

**目的：** 讓沒有全程參與過程的高層或關鍵 stakeholder 在短時間內做出決定，同時不被單一意見翻盤。
**時機：** 高風險、決策者只出現一次的場合（預算核准、對外承諾前的最後確認）。

**會前文件：Executive Pre-Wire Brief**
- 一句話商業目標錨點（連回 `project-brief.md` Problem）
- Swing vote 名單：這場會議裡意見還沒定、但有影響力的人是誰，會前先私下 1:1 對過
- Pregame huddle agenda：會議正式開始前 5 分鐘，跟 design advocate 對一次流程
- 預期會被問到什麼、要怎麼回應（可套 IDEAL Framework：Problem → Solution → User → Business → Lock in）

**依據：** Ch11 *How Executives Can Help Designers*（The King and the Blind Man）；Cheatsheet「若走進高風險高層會議：絕不單獨上陣，會前先在 1:1 對齊關鍵搖擺票，並開 5 分鐘 pregame huddle」。

---

## 🚚 Design-to-Dev Handoff

**目的：** 確保工程team拿到的是最新、狀態明確的交付物，而不是已經被推翻的舊版本。
**時機：** 一個 flow 或 spec 定案、準備開發前。

**會前文件：Handoff Checklist**
- 從 `deliverables.md` 抓要交付的項目，確認 Status 是 `Handed off` 而不是還卡在 `Draft` 或 `Stale`
- 從 `open-questions.md` 抓還沒解決但會擋開發的問題，標 urgency
- 交叉檢查：`design-decisions.md` 裡有沒有 `Superseded` 的決策，其對應交付物在 `deliverables.md` 裡還沒被標成 `Stale`——這種落差最容易讓工程做錯版本

**依據：** 不是 Greever 書中的獨立章節，但延續 Ch09 *Follow Up Afterward*「決策要落地成書面紀錄」的精神——handoff 是書面紀錄第一次被工程team拿去真的執行的時刻。

---

## ⏱️ Recurring Design Sync（週會／async check-in）

**目的：** 讓設計進度保持透明，避免累積一週後才發現方向偏了。
**時機：** 固定頻率的內部同步，非決策場合。

**會前文件：Status Digest**
- 從 `working-notes.md` 的 Informal Log／Still Exploratory 抓本週有進展或卡住的項目
- 列出目前擋住工作的 Open Questions（不重複列已經 resolved 的）
- 不需要完整簡報——這是同步場合，不是說服場合

**依據：** Cheatsheet trade-off「每日 30 分鐘 check-in vs 每週 design review」——選哪個頻率取決於專案風險，但無論哪種，會前準備的東西應該是「有變化的部分」，不是從頭重講一次。

---

## 🏁 Post-Launch Retro

**目的：** 對照 Kickoff 設下的成功指標，檢視實際結果，並把值得留下的知識往上收斂。
**時機：** 交付上線後、有足夠數據可以看結果時。

**會前文件：Outcome Review Brief**
- 對照 `FOLDER-INSTRUCTIONS.md` Layer 4 的成功指標，逐項填「達成 / 未達成 / 還無法判斷」
- 從 `changelog.md` 重建這個專案實際走過的時間線
- 從 `deliverables.md` 確認最終交付了什麼版本
- 標出哪些決策事後看是對的、哪些該 `#promote` 到 `pattern-library.md`（見 `FOLDER-INSTRUCTIONS.md` Layer 2.5）

**依據：** 呼應書中 Bank Account of Trust 的概念（Ch10）——retro 是把這次專案的信任餘額（做對的事）跟虧損（做錯的事）都記下來，供下一個專案借鏡。

---

## 沒有涵蓋到的會議

如果你要開的會議不在上面六種裡，不要硬套——先問自己：這場會議的目的是「定義問題」「換取回饋」「爭取決定」「交接」「同步狀態」還是「回顧結果」？多半能對到上面某一種的變體。真的對不到，就照 Ch03 Setting the Context 的通用開場（目標、上次結論、時間軸、要什麼回饋、再說一次目標）自己搭一份，不必等這份文件更新。
