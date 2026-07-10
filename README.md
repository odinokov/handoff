# handoff

A [Claude Code](https://claude.com/claude-code) skill that writes or updates `./HANDOFF.md` — a minimal, executable session handoff (Goal, Current Progress, What Worked, What Didn't Work, Next Steps) so a fresh agent can continue the work with zero prior context. It touches that one file and nothing else; on re-runs it updates the existing handoff instead of starting over.

## Install

**Personal** — available in every project on this machine:

```bash
git clone https://github.com/odinokov/handoff.git ~/.claude/skills/handoff
```

Update with `git -C ~/.claude/skills/handoff pull`.

**Project** — committed to a repo. Don't nest a clone inside your repo (git records it as a gitlink, not files); copy the skill file instead:

```bash
mkdir -p .claude/skills/handoff
curl -fsSL https://raw.githubusercontent.com/odinokov/handoff/HEAD/SKILL.md \
  -o .claude/skills/handoff/SKILL.md
```

Restart Claude Code; the skill is available as `/handoff`.

## Usage

Invoke `/handoff` — or just say you're wrapping up; it triggers automatically. Claude writes (or updates) `./HANDOFF.md` and stops.

To resume, start a fresh agent session in the same repo root and paste the file's final line as its first instruction:

```
Bootstrap: Read ./HANDOFF.md, start at §5 Next Steps.
```
