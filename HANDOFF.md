# HANDOFF

## 1. Goal

- Publish the `handoff` Claude Code skill as a public GitHub repo `odinokov/handoff`.
- Done when: anonymous `git clone https://github.com/odinokov/handoff.git` works and matches local HEAD.
- Out of scope: editing SKILL.md content (finalized), changing the local install in `~/.claude/skills/handoff/`.

## 2. Current Progress

- Repo: `/home/denis/tools/handoff`, branch `main` tracking `origin/main`, single-commit history pushed to `git@github.com:odinokov/handoff.git`.
- Remote repo exists but is **private** — anonymous access returns HTTP 404, so README's clone/curl instructions don't work for others yet.
- Skill installed and verified working: `~/.claude/skills/handoff/` (plain file copy).

## 3. What Worked

- Extracting the GitHub token: `awk '/oauth_token/{print $2; exit}' ~/.config/gh/hosts.yml` (file has two token lines; take the first only).
- Pushing over SSH: `git push -u origin main` with the `git@github.com:` remote.

## 4. What Didn't Work

- `grep oauth_token ~/.config/gh/hosts.yml | awk '{print $2}'` — returns two tokens; the embedded newline malforms the auth header and curl fails with exit 43 / HTTP 000.
- HTTPS git remotes in this environment — credential prompts fail; always use SSH.
- Don't run git commands in `~/.claude/skills/handoff/` (plain copy, not a clone) or from `/home/denis/tools/` (broken `.git` stub) — use `git -C /home/denis/tools/handoff`.

## 5. Next Steps

- Make the repo public:
  ```bash
  TOKEN=$(awk '/oauth_token/{print $2; exit}' ~/.config/gh/hosts.yml)
  curl -s -o /dev/null -w "%{http_code}" -X PATCH -H "Authorization: token $TOKEN" \
    -d '{"private":false}' https://api.github.com/repos/odinokov/handoff
  ```
- Expected: prints `200`, then `curl -s -o /dev/null -w "%{http_code}" https://github.com/odinokov/handoff` prints `200`. Stop when observed, or after one failed attempt (record it in §4).

Bootstrap: Read ./HANDOFF.md, start at §5 Next Steps.
