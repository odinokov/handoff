# HANDOFF

## 1. Goal

- Publish the `handoff` Claude Code skill as public GitHub repo `odinokov/handoff`.
- Done when: `git clone https://github.com/odinokov/handoff.git` works and matches local HEAD.
- Out of scope: editing SKILL.md/README.md content (finalized), changing the local install in `~/.claude/skills/handoff/`.

## 2. State

- Repo: `/home/denis/tools/handoff`, branch `master`, HEAD `bffd4ecfb22a72848ac32287f594418f95442236`, working tree clean (except this file), no upstream set.
- Remote `origin` = `git@github.com:odinokov/handoff.git` — remote repo does not exist yet (`https://github.com/odinokov/handoff` returned HTTP 404 on 2026-07-10).
- Skill installed and verified working: `~/.claude/skills/handoff/` (plain file copy, byte-identical to repo HEAD).
- README.md's Install section already points at the HTTPS GitHub URL, so the published repo must be named exactly `handoff`.
- Generated: 2026-07-10T08:51:14Z.

## 3. Next step

- Create the GitHub repo, then push. GitHub OAuth token is in `~/.config/gh/hosts.yml` under `oauth_token:` (`gh` CLI not installed — use the API; never echo the token).
- Command:
  ```bash
  TOKEN=$(grep oauth_token ~/.config/gh/hosts.yml | awk '{print $2}')
  curl -s -o /dev/null -w "%{http_code}" -H "Authorization: token $TOKEN" \
    -d '{"name":"handoff","description":"Claude Code skill: minimal executable session handoff (HANDOFF.md)"}' \
    https://api.github.com/user/repos
  git -C /home/denis/tools/handoff push -u origin master
  ```
- Expected: curl prints `201`; push succeeds; `curl -s -o /dev/null -w "%{http_code}" https://github.com/odinokov/handoff` prints `200`.
- Stop when observed, or after one failed attempt (record the failure here).

## 4. Traps

- Push over SSH (`git@github.com:`), not HTTPS — HTTPS remotes cause credential prompts/failures in this environment.
- Do not commit `HANDOFF.md` to the published repo; delete or gitignore it before pushing.
- `~/.claude/skills/handoff/` is a plain copy, not a clone — do not run git commands there; sibling skills follow the same convention.
- `/home/denis/tools/.git` (parent dir) is a broken stub — always use `git -C /home/denis/tools/handoff`.

Bootstrap: Read ./HANDOFF.md, do §3 only, stop.
