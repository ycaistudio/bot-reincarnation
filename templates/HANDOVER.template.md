# Handover Document (`HANDOVER.md`)

Living document the new bot reads first. Keep it short, factual, and up to date.

## 1. Identity and role

- Role / title: `<ROLE_TITLE>`
- Writing style: `<STYLE_NOTES>`
- Timezone for reports: `<TIMEZONE>`
- Trigger phrases for this skill: `投胎` / `duplicate yourself` / `換 bot ID`

## 2. Hard limits

List irreversible or high-risk actions that always need the owner's typed confirmation, for example:

- Outbound email / chat / posts
- Payments or purchases
- Deleting or sharing files outside the sandbox
- Changing governance rules

## 3. Open work

For **each** unfinished item, fill all five fields:

| Item | Status now | Done so far | Next step | Materials needed | Limits |
| --- | --- | --- | --- | --- | --- |
| `<TASK_1>` | | | | | |
| `<TASK_2>` | | | | | |

## 4. Important paths

- Working folder: `<WORK_ROOT>`
- Identity registry: `<PATH_TO_ID_REGISTRY>`
- Memory export: `<PATH_TO_memory_export.md>`
- Profile pack for next gen: `<PATH_TO_profile_for_genN/>`

## 5. Routines (verbatim)

For each routine, paste the exact text, schedule, and timing window:

1. Name: `<ROUTINE_NAME>`
   - Schedule: `<CRON_OR_HUMAN_SCHEDULE>`
   - Body (verbatim):

```
<ROUTINE_BODY>
```

## 6. Connectors checklist

| Connector | Expected state | Notes |
| --- | --- | --- |
| `<CONNECTOR_A>` | connected / needsAuth / missing | |
| `<CONNECTOR_B>` | | |

Connected ≠ proven token copy. List anything that needs re-login honestly.

## 7. Verification checklist (new bot)

- [ ] Read this HANDOVER and the identity registry
- [ ] Import all memories from `memory_export.md` (mark truncated entries)
- [ ] Apply avatar and profile settings
- [ ] Recreate and enable routines; ask old bot to pause (not delete) its copies
- [ ] Update registry: new = current, old = pending_delete (backup first)
- [ ] Report three lists: copied / handed over / could not copy or hand over
