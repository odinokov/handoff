# HANDOFF

## 1. Goal

- Ship README audit fixes for `odinokov/handoff`: MIT license, example link to this file, update notes for project installs, corrected Codex reload wording.
- Done when: `README.md`, `LICENSE`, `HANDOFF.md` are committed and pushed to `origin/main`, and `https://raw.githubusercontent.com/odinokov/handoff/HEAD/LICENSE` returns HTTP 200.
- Out of scope: editing `SKILL.md` (finalized).

## 2. Current Progress

- Repo: `/home/denis/tools/handoff`, branch `main`, HEAD `16a4e505c5b20441d4a0e375083079ce41e53cb5` = `origin/main`; repo is public.
- Uncommitted: `README.md` (modified), `LICENSE` (new, MIT, "Copyright (c) 2026 Denis Odinokov"), `HANDOFF.md` (modified).
- README install claims verified: clone URL and raw `SKILL.md` URL return 200; raw `SKILL.md` is byte-identical to local; Codex paths and `$handoff` match https://developers.openai.com/codex/skills.
- Claude Code install `~/.claude/skills/handoff/`: plain file copy, `SKILL.md` identical to repo.
- Codex install `~/.agents/skills/handoff/`: fresh `git clone` at `16a4e50`; Codex detects it (see §3).

## 3. What Worked

- Extracting the GitHub token: `awk '/oauth_token/{print $2; exit}' ~/.config/gh/hosts.yml` (file has two token lines; take the first only).
- Pushing over SSH: `git push -u origin main` with the `git@github.com:` remote.
- Making the repo public: `curl -X PATCH -H "Authorization: token $TOKEN" -d '{"private":false}' https://api.github.com/repos/odinokov/handoff` → 200.
- Verifying Codex sees the skill (run from a non-repo dir): `codex exec --skip-git-repo-check -s read-only "Do not use any tools. Is a skill named 'handoff' in your available skills list? Answer only YES or NO, then the path to its SKILL.md if listed."` → `YES /home/denis/.agents/skills/handoff/SKILL.md` (codex-cli 0.149.0).

## 4. What Didn't Work

- `grep oauth_token ~/.config/gh/hosts.yml | awk '{print $2}'` — returns two tokens; the embedded newline malforms the auth header and curl fails with exit 43 / HTTP 000.
- HTTPS git remotes for push in this environment — credential prompts fail; always use SSH. (Anonymous HTTPS clone works.)
- Don't run git commands in `~/.claude/skills/handoff/` (plain copy, not a clone) or from `/home/denis/tools/` (broken `.git` stub) — use `git -C /home/denis/tools/handoff`.
- `~/.agents/skills/handoff/` previously held only a stray `HANDOFF.md` and no `SKILL.md`, so Codex didn't load the skill; it is now a clone — update it with `git -C ~/.agents/skills/handoff pull`, don't copy files into it.

## 5. Next Steps

- Commit and push (user approval required):
  ```bash
  git -C /home/denis/tools/handoff add README.md LICENSE HANDOFF.md
  git -C /home/denis/tools/handoff commit -m "Add MIT license; README: example link, update notes, Codex reload wording"
  git -C /home/denis/tools/handoff push
  curl -s -o /dev/null -w "%{http_code}\n" https://raw.githubusercontent.com/odinokov/handoff/HEAD/LICENSE
  ```
  Expected: push succeeds, curl prints `200` (raw CDN may lag a minute). Stop when observed, or after one failed attempt (record it in §4).
- Then sync the Codex clone: `git -C ~/.agents/skills/handoff pull` → fast-forward to the new HEAD.

Bootstrap: Read ./HANDOFF.md, start at §5 Next Steps.
