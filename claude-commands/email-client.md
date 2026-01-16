---
description: Send an email to a client (supports attachments and multiple recipients)
allowed-tools: Bash(resend-email:*), Bash(pandoc:*), Bash(wkhtmltopdf:*), AskUserQuestion, Read
---

Send an email using resend-email.

## Usage
```bash
resend-email -m "message body here" "recipient@example.com" "Subject" [attachments...]

# Multiple recipients (comma-separated)
resend-email -m "body" "a@x.com,b@y.com" "Subject" file.pdf
```

## Flow
1. Parse what user provided (recipients, subject, attachments, context)
2. Ask only for what's missing
3. If user wants files converted to PDF, do that first
4. Send using -m flag for the message body
5. Confirm when done

If user provides context in their message (like recipient emails or what to send), use it. Only ask for missing info.
