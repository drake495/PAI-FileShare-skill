# Drop Workflow

Copy one or more files to `~/Nextcloud/PAI-Drops/` for cloud sync.

## Steps

### 1. Identify Target File(s)

- If user specifies a path, use it directly
- If user says "that file" or "the file", identify from recent conversation context (last created/modified file)
- If ambiguous, use AskUserQuestion to clarify

### 2. Validate

- Confirm source file exists: `ls -la <source_path>`
- Confirm drop zone exists: `ls ~/Nextcloud/PAI-Drops/` (create with `mkdir -p` if missing)

### 3. Copy

For a single file:
```bash
cp "<source_path>" ~/Nextcloud/PAI-Drops/
```

For multiple files:
```bash
cp <file1> <file2> ... ~/Nextcloud/PAI-Drops/
```

For a directory:
```bash
cp -r "<source_path>" ~/Nextcloud/PAI-Drops/
```

**If filename collision exists**, prepend timestamp:
```bash
cp "<source_path>" ~/Nextcloud/PAI-Drops/$(date +%Y%m%d-%H%M%S)_$(basename "<source_path>")
```

### 4. Verify

```bash
ls -lh ~/Nextcloud/PAI-Drops/$(basename "<source_path>")
```

### 5. Report

Confirm to user:
- Filename copied
- File size
- Location: `~/Nextcloud/PAI-Drops/<filename>`
- Reminder: "It will sync automatically to your Nextcloud devices"
