# Identity Registry (`ID_REGISTRY.md`)

Track every generation of this bot role. Permissions should follow **who is current / in handover** in this registry, not a hard-coded bot ID.

| Gen | Bot ID | Display name | Created (timezone) | Status | Handed over by | Authorization message |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | `<BOT_ID_GEN1>` | `<DISPLAY_NAME>` | `<YYYY-MM-DD HH:MM TZ>` | current | — | `<OWNER_CONFIRM_MSG_REF>` |
| 2 | `<BOT_ID_GEN2>` | `<DISPLAY_NAME> (2)` | `<YYYY-MM-DD HH:MM TZ>` | handover | Gen1 | `<OWNER_CONFIRM_MSG_REF>` |

## Status values

- `current` — active incumbent
- `handover` — newly created; inheritance in progress
- `pending_delete` — incumbent confirmed; waiting for owner to delete manually
- `retired` — owner deleted the old bot; recorded for history

## Rules

1. Fill the **real** new bot ID immediately after `CreateAgent`. Never leave placeholder text.
2. Backup this file (with a timestamped copy) before every status change.
3. Only the owner may delete a bot. Bots never delete bots.
4. After the owner deletes the old bot, mark it `retired` and note the time.
