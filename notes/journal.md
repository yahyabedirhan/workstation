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

## 2026-09-20

Tried running several Claude Code sessions on one repo at once, each in its own git worktree, driven from a single herdr pane. Written up as [herdr-treehouse-worktrees](concepts/herdr-treehouse-worktrees.md).

What happened:

- Controlled herdr from inside an agent pane using the JSON CLI: created tabs with `--cwd` and `--no-focus`, started agents with `herdr agent start`, prompted all three in parallel, waited, read output, closed tabs. The `/herdr` skill in `~/.claude/skills/herdr` covers the rest of the CLI.
- Installed treehouse. `go install github.com/kunchenguid/treehouse@latest` gave v1.8.0 because the module path has no `/v2` suffix. Downloaded the v2.3.0 darwin-arm64 release binary into `~/go/bin/treehouse` by hand and added `export PATH="$HOME/go/bin:$PATH"` to `~/.zshrc`. Skipped the official `install.sh`: `~/.local/bin` is not on PATH so it would have picked `/usr/local/bin` with sudo.
- Three leases (`treehouse get --lease --lease-holder cc-wtN --json`) created a pool at `~/.treehouse/<repo>-<hash>/<N>/<repo>`, detached HEAD at `main`. Each agent wrote an untracked demo file that landed only in its own worktree; the main checkout stayed clean. `treehouse status` showed the pids in each slot.
- Cleanup was `herdr tab close` per tab then `treehouse return --force <path>` per worktree. `return --all` from the README is not in v2.3.0.

Decisions:

- `zstyle ':omz:update' mode auto` before sourcing oh-my-zsh: the update prompt was swallowing the first keystrokes typed into a fresh pane, so `claude` became the answer to the prompt instead of a command.

Revisit:

- How branches from worktrees flow back (PR per worktree, or merge into the main checkout).
- Set up `treehouse.toml` or `.worktreeinclude` so gitignored files like `node_modules` get seeded; decide the list per repo.
- Whether `--lease-holder` should encode the herdr pane or agent name so `treehouse status` and `herdr agent list` line up.
- `herdr agent read` cannot recover output scrolled off the alternate screen; the fallback is asking the agent to write to a file. Look for a better way.
