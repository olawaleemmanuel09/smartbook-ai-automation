# Security Policy

## Reporting a vulnerability

If you find a security issue in this repository — including, but not limited to, accidentally committed credentials, hardcoded secrets, or any sensitive data that shouldn't be public — please **do not open a public issue**.

Instead, email **olawaleemmanuel100@gmail.com** with the details. I'll respond within 48 hours and patch the issue immediately.

---

## What this repository does NOT contain

This repository contains **no live credentials**. Every secret has been replaced with a `{{PLACEHOLDER}}` marker. Specifically, the workflow JSON does not contain:

- API keys (Anthropic, OpenAI, Twilio, etc.)
- Database credentials (Supabase service role keys, JWT tokens)
- SMTP passwords
- Webhook secrets
- Production URLs (Supabase project URL, custom domains)
- Personal data (real email addresses, real phone numbers)

If you spot any of the above in a commit, please report it via the email above. I treat credential exposure as a P0 incident.

---

## Credential management approach

This project follows a simple set of rules:

1. **Never hardcode credentials.** All secrets live in `.env` (local) or n8n's credential store (production).
2. **`.env` is in `.gitignore`** and has never been committed.
3. **The workflow JSON uses placeholders.** When importing into your own n8n instance, you connect the nodes to your own credentials.
4. **n8n credential IDs are stripped** from the exported workflow. The IDs are environment-specific and would be useless to an attacker anyway, but they shouldn't be public.
5. **Production deployment** uses environment variables in Docker, not committed config files.

---

## If you fork this repo

Before running it with real credentials:

1. Copy `.env.example` to `.env` and fill in your own values
2. Confirm `.env` is in `.gitignore` (it is, but double-check)
3. Import the workflow into n8n and connect each credential node to your own n8n credentials
4. Test in a sandbox / dev project before pointing it at production data
