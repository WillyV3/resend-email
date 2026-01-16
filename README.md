# resend-email

Unix-style CLI for sending emails via Resend API. Pipe-friendly. Supports attachments.

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
# Basic
echo "Message body here" | resend-email recipient@example.com "Subject line"

# With attachment
echo "See attached" | resend-email recipient@example.com "Report" ./report.pdf

# Multiple attachments
echo "Files" | resend-email recipient@example.com "Documents" a.pdf b.png c.zip

# From a file
cat drafted-email.txt | resend-email client@example.com "Follow up"
```

Returns the Resend message ID on success, error message on failure.

## How it works

- Reads email body from stdin
- First arg is recipient
- Second arg is subject
- Remaining args are file paths to attach (base64 encoded)
- Config lives in `~/.config/resend/env`
