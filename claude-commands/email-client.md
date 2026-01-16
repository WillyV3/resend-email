---
description: Send an email to a client
allowed-tools: Bash(resend-email:*), AskUserQuestion
---

Ask the user for:
1. Recipient email address
2. Subject line
3. What they want to say (the message)

Then send using:
```bash
echo "<message>" | resend-email <recipient> "<subject>"
```

Confirm when sent. Keep it brief.
