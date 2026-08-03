# auto-apply-providers

First-party capability providers for the [auto-apply](https://github.com/yitaohou/auto-apply)
core plugin. Each provider is an independent plugin — install only what you need.
Every provider implements a contract from the core's `contracts/` directory and
installs exactly the way a third-party provider does.

| Plugin | Capability | Mailbox | Stack |
|---|---|---|---|
| `email-code-reader` | `email.verification_code@1` | Gmail | ego lite |

## email-code-reader

Reads a one-time ATS verification code from Gmail and returns it as a single line.
Contract: `contracts/email.verification_code.v1.md` in the core repository.

### Access setup (required before first use)

This provider reads Gmail **through ego lite's browser session** — it holds no
credentials of its own and will never attempt to log in.

- **Log into the Gmail account in ego lite yourself, once.** The provider reuses
  that session from then on.
- If the session expires or the account raises a challenge, the provider returns
  `ERR MAILBOX_UNREACHABLE`; log in again in ego lite to restore it.

### Install and bind

1. Install the `email-code-reader` plugin from this repository (or let the core's
   provider registration flow do it after your confirmation)
2. Bind it in the core's `data/providers.csv`:

       capability,provider_agent,enabled,notes
       email.verification_code@1,email-code-reader,on,Gmail via ego lite

3. Set `email_access = read_only` and fill `email_address` in `settings.csv`
   (registration asks these for you)
4. Restart the session — agent definitions load at startup. Confirm with `/agents`
