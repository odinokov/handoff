# handoff

A [Claude Code](https://claude.com/claude-code) and [OpenAI Codex](https://developers.openai.com/codex/) skill that writes or updates `./HANDOFF.md` — a minimal, executable session handoff (Goal, Current Progress, What Worked, What Didn't Work, Next Steps) so a fresh agent can continue the work with zero prior context. It touches that one file and nothing else; on re-runs it updates the existing handoff instead of starting over.

## Install in Claude Code

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

## Install in OpenAI Codex

**Personal** — available in every project on this machine:

```bash
git clone https://github.com/odinokov/handoff.git ~/.agents/skills/handoff
```

Update with `git -C ~/.agents/skills/handoff pull`.

**Project** — commit the skill with the repository. Copy the file rather than nesting a clone inside the repo:

```bash
mkdir -p .agents/skills/handoff
curl -fsSL https://raw.githubusercontent.com/odinokov/handoff/HEAD/SKILL.md \
  -o .agents/skills/handoff/SKILL.md
```

Restart Codex or start a new session. Invoke the skill with `$handoff`, or ask Codex to write a handoff; it can select the skill automatically when the request matches its description.

## Usage

In Claude Code, invoke `/handoff`. In Codex, invoke `$handoff`. You can also say you're wrapping up; the agent can select the skill automatically. It writes (or updates) `./HANDOFF.md` and stops.

To resume, start a fresh agent session in the same repo root and paste the file's final line as its first instruction:

```
Bootstrap: Read ./HANDOFF.md, start at §5 Next Steps.
```
