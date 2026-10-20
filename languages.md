# Implementations

Every repo that speaks this contract. The fan-out in [`AGENTS.md`](AGENTS.md) spawns one subagent per
row.

| Repo | Role | Status | Runtime token | Vendored fixtures |
|---|---|---|---|---|
| `replypen` | **host** — the other side of every plane | live | — | private conformance fixtures |
| `replypen-embassy-ruby` | Ruby Embassy (Rails/Rack), gem `replypen-embassy` | v0.17.0 (hub 9aa0bfc, consumed from git main); action/analysis/chat/API parity + typed diagnostics | `ruby` (in-process eval) | `spec/fixtures/contract/` |
| `replypen-embassy-go` | Go Embassy, module `github.com/replypen/replypen-embassy-go` | live, 0.8.0 (hub 9aa0bfc) | `go` (yaegi) | `internal/contract/testdata/` |
| PHP | Laravel/Symfony Embassy | planned | `php` | — |
| `replypen-embassy-python` | Python Embassy (Litestar/FastAPI/Django), package `replypen_embassy`, `github.com/replypen/replypen-embassy-python` | live, 0.7.0 (hub 9aa0bfc) | `python` (via registered runner, decision 12) | `tests/contract/testdata/` |
| Node | Express/Nest Embassy | planned | `node` | — |

## Per-plane coverage

| | actions | dry_run | analysis trigger | trigger `credentials` | result callback | sent-message | answers | chat mint | chat `credentials` | api plane | health |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| host | ✅ | ✅ | ✅ | pending | ✅ | ✅ | ✅ | verify only | verify + inject | ✅ | — |
| ruby | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| go | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ ¹ | ✅ |
| python | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

¹ Go implements the API plane; its API-plane conformance cases are not ported yet.

## Adding a language

1. Add the row above and its runtime token to [decision 8](decisions.md#8-runtime-tokens).
2. Vendor `fixtures/` + the hub SHA.
3. Implement, in this order: signing → replay → schema → resolve → execute → result envelope →
   analysis planes → chat mint → api plane → health.
4. Conformance suite per [`AGENTS.md`](AGENTS.md) rule 3, wired into CI.
5. Create the public `replypen/<repo>` GitHub repo, add its SSH `origin`, push full `main`, and
   verify local `HEAD == origin/main` plus a clean worktree. If the task explicitly forbids this,
   record publication as pending in the implementation row and handoff.
