---
name: FileShare
description: Share files via Nextcloud sync. USE WHEN send file, drop file, share file, send me that, grab file, nextcloud, file to phone, file to cloud.
---

## Customization

**Before executing, check for user customizations at:**
`~/.claude/skills/PAI/USER/SKILLCUSTOMIZATIONS/FileShare/`

If this directory exists, load and apply any PREFERENCES.md, configurations, or resources found there. These override default behavior. If the directory does not exist, proceed with skill defaults.


## MANDATORY: Voice Notification (REQUIRED BEFORE ANY ACTION)

**You MUST send this notification BEFORE doing anything else when this skill is invoked.**

1. **Send voice notification**:
   ```bash
   curl -s -X POST http://localhost:8888/notify \
     -H "Content-Type: application/json" \
     -d '{"message": "Running the WORKFLOWNAME workflow in the FileShare skill to ACTION"}' \
     > /dev/null 2>&1 &
   ```

2. **Output text notification**:
   ```
   Running the **WorkflowName** workflow in the **FileShare** skill to ACTION...
   ```

**This is not optional. Execute this curl command immediately upon skill invocation.**

# FileShare

Copy files to `~/Nextcloud/PAI-Drops/` for automatic cloud sync and remote access.

## Drop Location

**Target:** `~/Nextcloud/PAI-Drops/`

Nextcloud client syncs this folder automatically. Files appear on all connected devices (phone, laptop, web UI).

## Workflow Routing

| Trigger | Workflow |
|---------|----------|
| "send me that file", "drop file", "share file", "send to nextcloud" | `Workflows/Drop.md` |
| "list shared files", "what's in PAI-Drops" | `Workflows/List.md` |

## Quick Reference

- **Drop zone:** `~/Nextcloud/PAI-Drops/`
- **Sync:** Automatic via Nextcloud client
- **Access:** Nextcloud web UI, mobile app, or any synced device
- Copies files (does not move) — originals stay in place
- Timestamped copies avoid filename collisions

## Examples

**Example 1: Share a file just created**
```
User: "send me that file"
→ Identifies most recently created/modified file in context
→ Copies to ~/Nextcloud/PAI-Drops/
→ Confirms with filename and size
```

**Example 2: Drop a specific file**
```
User: "drop ~/Alice/output/report.pdf to nextcloud"
→ Copies report.pdf to ~/Nextcloud/PAI-Drops/
→ Confirms copy with ls verification
```
