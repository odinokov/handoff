---
name: handoff
description: Create a minimal, executable session handoff (./HANDOFF.md) so a fresh agent can resume work with zero prior context. Use this skill whenever the user wants to wrap up, pause, or end a session, hand off work to another agent or a new session, "save state", "write a handoff", "document where we are", "leave notes for next time", or continue this work later — even if they don't say the word "handoff". Also use it before context runs out on long tasks when the user asks to preserve progress.
---

# Session Handoff

Create `./HANDOFF.md` — the only file you may create or modify. Read-only inspection is allowed. Don't change source, config, Git state, or do the next agent's work.

## Rules

- Zero-context reader: record state, not history. One fact per bullet.
- Exact paths, SHAs, commands, errors — verbatim. Never invent; mark guesses `UNVERIFIED:`. Redact secrets.
- Write `None.` when a section is empty.

## Sections

1. **Goal** — outcome, definition of done, out of scope.
2. **State** — branch + HEAD SHA, dirty files, what works, what's broken.
3. **Next step** — one bounded change, exact command, expected result. Stop when observed, or after one failed attempt (record the failure here).
4. **Traps** — dead ends already tried, invariants not to break, files that look relevant but must not be touched.

## Ending

End the file exactly with:

`Bootstrap: Read ./HANDOFF.md, do §3 only, stop.`
