---
name: handoff
description: Write or update a handoff document (./HANDOFF.md) so the next agent with fresh context can continue this work. Use this skill whenever the user wants to wrap up, pause, or end a session, hand off work to another agent or a new session, "save state", "write a handoff", "document where we are", "leave notes for next time", or continue this work later — even if they don't say the word "handoff". Also use it before context runs out on long tasks when the user asks to preserve progress.
---

# Session Handoff

Write or update `./HANDOFF.md` — the only file you may create or modify. Read-only inspection is allowed. Don't change source, config, Git state, or do the next agent's work.

## Steps

1. If `./HANDOFF.md` already exists, read it first — then update it: keep entries that are still true, prune stale ones.
2. Write the sections below.
3. Tell the user the file path, so a fresh conversation can start with just that path.

## Rules

- Zero-context reader: record state, not history. One fact per bullet.
- Exact paths, SHAs, commands, errors — verbatim. Never invent; mark guesses `UNVERIFIED:`. Redact secrets.
- Write `None.` when a section is empty.

## Sections

1. **Goal** — what we're trying to accomplish: outcome, definition of done, out of scope.
2. **Current Progress** — what's done so far: branch + HEAD SHA, dirty files, what works, what's broken.
3. **What Worked** — approaches that succeeded, with the exact commands.
4. **What Didn't Work** — failed approaches and exact errors, so they're not repeated; invariants not to break; files that look relevant but must not be touched.
5. **Next Steps** — clear action items for continuing; make the first one bounded: exact command, expected result. Stop when observed, or after one failed attempt (record it in §4).

## Ending

End the file exactly with:

`Bootstrap: Read ./HANDOFF.md, start at §5 Next Steps.`
