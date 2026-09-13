# Journal

One section per day. What changed, why, and what to revisit. Configuration itself lives in [tools/](../tools/index.md); this file is the reasoning around it.

## 2026-09-13

Started this repo as the meta project for my environment: every other project points here for agent rules, skills and tool setup.

Decisions:

- Agent-readable markdown over install scripts. Scripts break across macOS and Linux; a doc an agent can follow adapts. Promote a step to a script only after doing it by hand twice.
- One folder per tool with a lowercase `index.md` that only points at files, like an `index.ts`.
- Skills treated like `node_modules`: vendored in `.agents/skills/`, pinned in `skills-lock.json`, symlinked into `.claude/skills/`.
- Default skill set is all of `mattpocock/skills` plus `show-me` and `i-have-adhd`.
- Global Claude Code settings are safety rails (`deny`/`ask`); project settings are `allow` lists only.
- Secrets guard is a rule, not an agent habit: gitleaks pre-commit hook with pattern-only rules (any home path, any email, any IPv4), plus a GitHub Action.
- Switched terminal from iTerm2 to Ghostty so its tabs and keybindings stop colliding with herdr's `ctrl+b` prefix.
- Hetzner VPS plus herdr for 24/7 agents: the VPS is the always-on machine, SSH is how you reach it, herdr is what keeps the session alive after you leave.

Revisit:

- Whether `template/` needs to become `templates/<kind>/` once a second template appears.
- Fill `notes/concepts/` after reviewing the async-starter explainers.
