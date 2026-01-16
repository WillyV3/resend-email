---
description: Send an email to a client (supports attachments and multiple recipients)
allowed-tools: Bash(resend-email:*), Bash(pandoc:*), Bash(wkhtmltopdf:*), Bash(cat:*), Bash(echo:*), AskUserQuestion, Read
---

Send an email using resend-email.

## Capabilities
- Multiple recipients: send same email to each
- Attachments: any file type (PDFs, images, docs, etc.)
- PDF conversion: convert markdown/text to PDF before attaching

## Usage
```bash
# Basic
echo "<message>" | resend-email <recipient> "<subject>"

# With attachments (additional args after subject)
echo "<message>" | resend-email <recipient> "<subject>" file1.pdf file2.png

# Multiple recipients: run once per recipient
```

## Flow
1. Parse what user provided (recipients, subject, attachments, context)
2. Ask only for what's missing
3. If user wants files converted to PDF, do that first
4. Send to all recipients
5. Confirm when done

If user provides context in their message (like recipient emails or what to send), use it. Only ask for missing info.
