# resend-email

Unix-style CLI for sending emails via Resend API. Pipe-friendly. Supports attachments and multiple recipients.

## Setup

1. Get an API key from [resend.com](https://resend.com)

2. Create config:
```bash
mkdir -p ~/.config/resend
chmod 700 ~/.config/resend

cat > ~/.config/resend/env << 'EOF'
RESEND_API_KEY=your_api_key_here
RESEND_FROM=you@yourdomain.com
EOF

chmod 600 ~/.config/resend/env
```

3. Install:
```bash
cp resend-email ~/.local/bin/
chmod +x ~/.local/bin/resend-email
```

Requires `jq` and `curl`.

## Usage

```bash
# Basic (using -m flag)
resend-email -m "Message body here" recipient@example.com "Subject line"

# Multiple recipients (comma-separated, max 50)
resend-email -m "Hey team" "alice@x.com, bob@y.com" "Update"

# With attachment
resend-email -m "See attached" recipient@example.com "Report" ./report.pdf

# Multiple attachments
resend-email -m "Files" recipient@example.com "Documents" a.pdf b.png c.zip

# Pipe from file (alternative to -m)
cat drafted-email.txt | resend-email client@example.com "Follow up"
```

Returns the Resend message ID on success, error message on failure.

## Claude Code Integration

If you use [Claude Code](https://claude.ai/code), you can have Claude send emails for you.

### Install the command

```bash
cp claude-commands/email-client.md ~/.claude/commands/
```

### Use it

```
/email-client
```

Claude will ask for the recipient, subject, and message, then send it.

### Build your own commands

The script is pipe-friendly, so you can create custom Claude commands for specific workflows:

```markdown
---
description: Send weekly report to team
allowed-tools: Bash(resend-email:*)
---

Send the weekly status report.

Ask user for the report content, then send to team@company.com with subject "Weekly Status Report - [date]"
```

## How it works

- `-m "body"` flag for message body (or pipe to stdin)
- First positional arg is recipient(s) - comma-separated for multiple (max 50)
- Second positional arg is subject
- Remaining args are file paths to attach (base64 encoded)
- Config lives in `~/.config/resend/env`
