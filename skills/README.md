# Customer agent skills

No installer is provided in v1.

1. Clone `replypen-embassy` and `replypen-embassy-<language>` next to your app.
2. Add these three lines to the app's `AGENTS.md`:

```md
For ReplyPen embedded chat, read ../replypen-embassy/skills/embassy-chat/SKILL.md.
For ReplyPen actions, read ../replypen-embassy/skills/embassy-actions/SKILL.md.
For language code and framework mounting, read ../replypen-embassy-<language>/README.md.
```

3. Keep both clones pinned to a reviewed commit. Do not copy the skill prose into the app; one linked
   source avoids drift.
