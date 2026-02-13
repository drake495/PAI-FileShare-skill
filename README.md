# FileShare Skill

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that copies files to a Nextcloud sync folder for automatic cloud access across all your devices.

## What It Does

When you say things like "send me that file" or "drop this to Nextcloud", the skill copies files to `~/Nextcloud/PAI-Drops/`. The Nextcloud client syncs that folder automatically, making files available on your phone, laptop, web UI, or any connected device.

Files are copied, not moved — originals stay in place. Filename collisions are handled with timestamps.

## Workflows

### Drop

Copies one or more files to the drop folder.

**Triggers:** "send me that file", "drop file", "share file", "send to nextcloud"

**What it does:**
1. Identifies the target file (from your explicit path or recent conversation context)
2. Validates the source exists and creates the drop folder if needed
3. Copies the file (with timestamp prefix if a collision exists)
4. Verifies the copy and reports filename + size

### List

Shows what's currently in the drop folder.

**Triggers:** "list shared files", "what's in PAI-Drops"

**What it does:**
1. Lists `~/Nextcloud/PAI-Drops/` sorted by date (newest last)
2. Shows filenames, sizes, and dates

## Setup

1. Install and configure the [Nextcloud desktop client](https://nextcloud.com/install/#install-clients)
2. Ensure `~/Nextcloud/` is your sync root (or adjust the path in `SKILL.md`)
3. Place this skill in your Claude Code skills directory (e.g., `~/.claude/skills/FileShare/`)

## Structure

```
FileShare/
  SKILL.md           # Skill definition and routing
  Workflows/
    Drop.md          # File copy workflow
    List.md          # List shared files workflow
```

## License

MIT
