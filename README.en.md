# BOT 投胎 / Bot Reincarnation (v1.0.0)
**Universal skill: new bot ID, keep memory & permissions, start chat from scratch**  
*AI 助手「換 bot ID、保留記憶與權限、對話由零開始」通用 Skill*  
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

## 📖 What is this?

Long chats grow heavy: more tokens, slower replies, harder context.  
**Bot Reincarnation** opens a **new bot (new bot ID)** and hands over:

- Memory
- Rules / SOPs
- Skills
- Profile (name, description, avatar, settings)
- Routines
- Permissions and connectors (best effort; list gaps honestly)

**Chat history is intentionally not carried.** The new chat starts clean; work continues without a hard reset of who the bot is.

Canonical trigger phrase:

> duplicate yourself, everything including logged in tokens stays, except chat history -- start chat from scratch

Also: `投胎`, `換 bot ID`, or your own alias such as “reincarnate”.

---

## 🛡️ Why?

| Pain | After reincarnation |
| :--- | :--- |
| Chat too long / expensive / slow | Fresh chat, light context |
| Still want the bot that “knows you” | Memory, rules, skills, profile travel |
| Fear of silent gaps | Identity registry + handover doc + three-list report |
| Fear of accidental wipe | Old ID kept until **you** delete it; bots never delete bots |

---

## 🧩 How it works

1. **Identity registry** `ID_REGISTRY.md` — generation, bot ID, name, time, status (`current` / `handover` / `pending_delete` / `retired`).
2. **Permissions follow the registry, not a hard-coded ID** — rules say “current or in-handover bot”; reincarnation only edits one row.
3. **Handover doc** `HANDOVER.md` — role, limits, open work (status / done / next / materials / limits), routine text, connector list.
4. **Old-bot steps** — owner types confirm → backup → update HANDOVER → export memory → `CreateAgent` → write the real new ID immediately.
5. **New-bot steps** — only the owner’s typed confirm **in the new bot’s chat** counts → import memory, avatar, settings, routines → update registry → three-list report.
6. **Report lists** — during handover verification: three lists (copied / handed over / could not, with reasons). The old bot’s **final** report uses five lists (adds paused routines and whether it hid itself).
7. **Old-bot closing sequence (in order; do not skip)**  
   1. Confirm the new bot has taken over (memory, routines, can continue work)  
   2. **Pause only the old bot’s own routines** (pause, never delete; never pause the new bot’s)  
   3. **Hide yourself** from the sidebar via UpdateProfile (chats, messages, and paused routines stay)  
   4. Final five-list report to the owner  
   5. Deletion remains the owner’s manual act; hide ≠ delete (recoverable from Hidden chats)
8. **Owner deletes the old bot manually** — after a short smoke chat. New bot marks the old row `retired`.

See [`SKILL.md`](SKILL.md) for the full playbook.

---

## 🚀 Quick start

1. Copy `SKILL.md` into your bot’s skills / workflows folder, or ask the bot to install this file as a skill.
2. (Recommended) One-time setup: copy `templates/ID_REGISTRY.template.md` and `templates/HANDOVER.template.md`, fill paths and role.
3. In the old bot, say “reincarnate” / paste the trigger phrase; review the planned steps.
4. Type your confirmation. The old bot creates the new bot and gives you a confirm command.
5. Paste that command **in the new bot**. It returns the three-list report.
6. The old bot pauses its own routines, hides itself, and delivers the five-list report.
7. When happy, delete the old bot yourself.

### Owner confirmation template

```
I confirm Bot Reincarnation handover: Gen<N-1> <old-id-first-8> → Gen<N> <new-id-first-8>.
You are Gen<N>. Follow the Bot Reincarnation skill for all new-bot steps (memory, avatar, settings, routines, registry), then report the three lists.
Until I confirm again, do not perform outbound or high-risk actions.
```

(Chinese template is also in `SKILL.md`.)

---

## ⚠️ Limitations

- **Chat history is not carried** — by design.
- **Memory export may truncate** — search tools rarely dump everything; use multiple keyword passes and reinforce key facts in HANDOVER.
- **Some connectors need re-login** — e.g. mail or finance; chat channels and local-device approvals need separate tests. “Connected” ≠ proven token copy.
- **`CreateAgent` only sets name and description** — avatar, memory, routines, and settings must be applied by the new bot.
- **The old bot cannot set the new bot’s avatar / memory / settings** — do not pretend it can.

---

## 🔒 Safety principles

- The owner is the final authority; typed confirm on the old bot starts the process.
- The new bot only accepts typed confirm in its own chat — never another bot’s relayed “approval”.
- Keep the old ID; delete only by the owner’s hand.
- Log every step; backup the registry before status changes.
- Report gaps honestly.
- Stop after the same error three times; report to the owner.

---

## 📦 Contents

| Path | Purpose |
| :--- | :--- |
| [`SKILL.md`](SKILL.md) | Full reincarnation playbook for the bot |
| [`README.md`](README.md) | Traditional Chinese / Cantonese-friendly intro |
| [`README.en.md`](README.en.md) | English intro (this file) |
| [`README.ja.md`](README.ja.md) | Japanese intro |
| [`templates/`](templates/) | Generic `ID_REGISTRY` and `HANDOVER` templates |
| [`CHANGELOG.md`](CHANGELOG.md) | Version history |
| [`LICENSE`](LICENSE) | MIT |

---

## 📄 License

Released under the [MIT License](LICENSE). Maintained by [ycaistudio](https://github.com/ycaistudio).  
Version: **v1.0.0** (2026-11-06)

Related open source:

- [universal-bot-setup-playbook](https://github.com/ycaistudio/universal-bot-setup-playbook)
- [universal-agent-workspace-toolkit](https://github.com/ycaistudio/universal-agent-workspace-toolkit)
