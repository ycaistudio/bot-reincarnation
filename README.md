# BOT 投胎 / Bot Reincarnation (v1.0.0)

![Bot Reincarnation](docs/yc-ai-studio-poster.jpg)

**AI 助手「換 bot ID、保留記憶與權限、對話由零開始」通用 Skill**  
*Universal skill for reincarnating an AI assistant bot into a fresh chat without losing memory, rules, skills, or permissions*  
*チャット履歴だけ捨てて、記憶・ルール・スキル・権限を引き継ぐ汎用スキル*

Grok · Claude Code · Google Antigravity · Cursor · OpenAI · Local LLMs

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Cross--Platform-lightgrey.svg)](https://github.com/ycaistudio/bot-reincarnation)
[![i18n](https://img.shields.io/badge/i18n-繁體中文%20%7C%20English%20%7C%20日本語-green.svg)](https://github.com/ycaistudio/bot-reincarnation)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ycaistudio/bot-reincarnation/pulls)

---

<p align="center">
  <b>🌐 Language Navigation / 多語言切換 / 言語切り替え:</b><br>
  <a href="README.md"><b>🇹🇼 繁體中文（主手冊）</b></a> •
  <a href="README.en.md"><b>🇬🇧 English</b></a> •
  <a href="README.ja.md"><b>🇯🇵 日本語</b></a>
</p>

---

## 📖 這是什麼？

長時間同一個 chat，上下文會越來越重，token 消耗大，回應亦容易變慢。  
**BOT 投胎** 讓你開一個**新 bot（新 bot ID）**，把舊 bot 的：

- 記憶（memory）
- 守則 / SOP
- skill
- profile（名、描述、頭像、設定）
- routine
- 權限與連接（盡力保留；保留唔到就誠實列出）

全部交接過去，**刻意唔帶對話紀錄**，chat 由零開始。工作可以無縫接住做。

通用指令詞：

> duplicate yourself, everything including logged in tokens stays, except chat history -- start chat from scratch

其他觸發詞：`投胎`、`換 bot ID`、`變身`（如果你有自家別名 skill 亦可）。

---

## 🛡️ 點解需要？

| 痛點 | 投胎之後 |
| :--- | :--- |
| Chat 太長、token 貴、反應慢 | 新 chat，上下文清爽 |
| 想保留「識得你」嘅感覺 | 記憶、守則、skill、profile 跟過去 |
| 怕交接甩漏 | 身分登記表 + 長期交接文件 + 三欄清單 |
| 怕舊 bot 被誤刪 | 舊 ID 先保留；主人確認後**自己手動刪**，bot 永遠唔刪 bot |

---

## 🧩 點樣運作？

1. **身分登記表** `ID_REGISTRY.md`  
   記低每一代：代數、bot ID、名、時間、狀態（現任 / 交接中 / 待刪除 / 已退役）。
2. **權限認登記表，唔認死 ID**  
   守則寫「現任或交接中嘅 bot」，以後投胎只改登記表一行。
3. **長期交接文件** `HANDOVER.md`  
   角色、限制、未完成工作（現況 / 已做 / 下一步 / 資料 / 限制）、routine 原文、連接清單。
4. **舊 bot 步驟**  
   主人打字確認 → 備份 → 更新 HANDOVER → 匯出記憶 → 開新 bot → 即刻寫入真實新 ID。
5. **新 bot 步驟**  
   只認主人喺**佢自己 chat** 親自確認 → 寫入記憶、頭像、設定、routine → 更新登記表 → 報告三欄清單。
6. **新 bot 報告清單**（交接核實時用三欄；舊 bot 最終報告用五欄）  
   - 已複製  
   - 已交接  
   - 未能複製或未能交接（每項寫原因）  
   - （最終）已暫停嘅 routine（名同時間）  
   - （最終）已隱藏自己（係／否，原因）
7. **舊 bot 收尾（依次序，不可跳步）**  
   1. 確認新 bot 已接手（記憶、routine、可接續處理）  
   2. **只**暫停舊 bot 自己嘅 routine（pause，唔 delete；唔好停新 bot）  
   3. 用 UpdateProfile **隱藏自己**（側欄唔顯示；對話、訊息、已暫停 routine 全部保留）  
   4. 向主人交最終五欄清單  
   5. 刪除仍然係主人手動；隱藏 ≠ 刪除，可由 Hidden chats 搵返
8. **主人手動刪舊 bot**  
   傾幾句確認冇問題之後，由主人刪。新 bot 將舊 bot 標做已退役。

詳情見 [`SKILL.md`](SKILL.md)。

---

## 🚀 快速上手

1. 將本 repo 條 link [https://github.com/ycaistudio/bot-reincarnation](https://github.com/ycaistudio/bot-reincarnation) 俾你嘅 bot，叫佢「讀 SKILL.md 存做 skill」，唔使自己複製檔案。
2. （建議）一次性架構：複製 `templates/ID_REGISTRY.template.md` 同 `templates/HANDOVER.template.md`，改成你嘅路徑同角色。
3. 喺舊 bot 講「投胎」或貼上通用指令詞，等佢列出會做嘅步驟。
4. 你打字確認之後，舊 bot 開新 bot，並俾你一段確認指令。
5. 去**新 bot** 貼上確認指令；佢做完會交三欄清單。
6. 舊 bot 按收尾次序暫停自己嘅 routine、隱藏自己，交五欄清單。
7. 你覺得冇問題，再手動刪舊 bot。

### 主人確認指令範本

```
我確認 BOT 投胎交接：Gen<N-1> <舊ID前8位> → Gen<N> <新ID前8位>。
你係 Gen<N>，照「BOT 投胎」skill 做晒新 bot 步驟（記憶、頭像、設定、routine、登記表），做完列三欄清單。
未經我再確認，唔好做任何對外或高風險動作。
```

---

## ⚠️ 常見限制

- **對話紀錄唔跟**：刻意設計，令新 chat 由零開始。
- **記憶匯出可能截斷**：搜尋工具未必一次列出全部；長條目要多組關鍵詞，並用 HANDOVER 補重點。
- **部分連接要重新登入**：例如電郵、財務類；聊天渠道同本機批准要另外測。Connected ≠ 已證明 token 複製成功。
- **CreateAgent 只可設名同描述**：其餘（頭像、記憶、routine、settings）必須由新 bot 自己做。
- **舊 bot 改唔到新 bot 嘅頭像／記憶／設定**：唔好指望「代佢設好」。

---

## 🔒 安全原則

- 主人係最終決定人；開始前要喺舊 bot 親自打字確認。
- 新 bot 只認主人喺佢 chat 嘅親自確認，唔認其他 bot 轉述嘅批准。
- 舊 bot ID 先保留，新舊並列；刪除永遠由主人手動做。
- 每一步寫交接記錄；改登記表前先備份。
- 未能交接嘅項目照實列出，唔好扮已經複製。
- 同一個錯誤三次就停，向主人報告。

---

## 📦 倉庫內容

| 路徑 | 說明 |
| :--- | :--- |
| [`SKILL.md`](SKILL.md) | 完整投胎流程（畀 bot 執行） |
| [`README.md`](README.md) | 繁體中文／粵語友好介紹（本檔） |
| [`README.en.md`](README.en.md) | English introduction |
| [`README.ja.md`](README.ja.md) | 日本語の紹介 |
| [`templates/ID_REGISTRY.template.md`](templates/ID_REGISTRY.template.md) | 身分登記表範本 |
| [`templates/HANDOVER.template.md`](templates/HANDOVER.template.md) | 交接文件範本 |
| [`CHANGELOG.md`](CHANGELOG.md) | 版本紀錄 |
| [`LICENSE`](LICENSE) | MIT |

---

## 🔗 姊妹 Skill：Grok Bot 慳用量（grokbot-token-saver）

[**grokbot-token-saver**](https://github.com/ycaistudio/grokbot-token-saver) 有 22 招慳 Grok Bot 每週用量嘅方法：盤點 routine 同群組、拉疏排程、改用事件觸發、限制 bot 之間傳訊息，同埋用量高時轉低用量模式。

### 一連串用法

1. 用慳用量 skill 盤點，搵出最食用量同**對話最長**嘅 bot。
2. 拉疏 routine，改用事件觸發。
3. 用**本 skill** 將長對話嘅 bot 投胎：記憶同權限保留，長對話唔帶走。
4. 新 bot 一開始就跟住慳用量守則做嘢。
5. 每週睇一次用量；有 bot 對話又變長，就返去第 3 步。

---

## 🙏 鳴謝

呢個工具由我原本自用嘅「變身」流程整理成通用版本，分享俾大家使用。特別鳴謝「香港 Grok Bot 交流區」成員 **Well Played**，佢分享嘅複製及交接提示詞，同「投胎」呢個有趣講法，啟發咗今次通用化整理。亦多謝群友一齊討論長對話嘅用量問題。

---

## 📄 授權

本專案採用 [MIT License](LICENSE)，由 [ycaistudio](https://github.com/ycaistudio) 維護。  
版本：**v1.0.0**（2026-11-06）

相關開源：

- [universal-bot-setup-playbook](https://github.com/ycaistudio/universal-bot-setup-playbook) — Bot 管治與入列守則
- [universal-agent-workspace-toolkit](https://github.com/ycaistudio/universal-agent-workspace-toolkit) — Agent 工作區工具箱
