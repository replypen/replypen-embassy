# Escalate an integration failure

Escalate when the error catalogue says **Who fixes: operator**, when all self-fix steps still produce
the same code, or when an action outcome is uncertain. Never retry an uncertain state-changing action.

## Capture a redacted bundle

Chat (`rp`, or `rc >= 1.22.0`):

```sh
rp project chat doctor --bundle
rp project chat doctor --origin https://app.acme.example --principal-kind acme_user --bundle
```

Actions — available today:

```sh
rp dev action doctor <action-id> --bundle
rp dev action doctor <action-id> --params '{"...":"..."}' --bundle   # exercise the real preflight
```

The chat bundle contains project slug, `rp` version, configuration state, principal-kind names, secret
source/status (never the value), branding booleans, redacted recent rejects, loader probe results,
findings, and timestamps. It must not contain secrets, token bytes, provider names, stack traces,
personal data, private host details, principal SQL, IP prefixes, or session ids. Review it before
sending.

## Message template

```text
To: support@replypen.com
Subject: ReplyPen integration failure: <CODE> for <project-slug>

Error line:
[ReplyPen] <CODE>: <hint> — <docs URL>

Redacted doctor bundle:
<paste JSON>

What I tried:
- <self-fix step>
- <result>

First observed: <UTC timestamp>
Environment: <staging or production; no credentials>
```

Attach no screenshots containing tokens and no raw `Authorization`, cookie, HMAC, or environment
values. If the bundle command itself fails, include `rp --version`, `rp auth access`, the command's
error line, and no credentials.
