# One agent per worktree with herdr and treehouse

Run several coding agents on the same repo at once without them stepping on each other's files. herdr owns the terminals, treehouse owns the git worktrees, and an agent in one pane can drive the rest.

## The two tools

- [herdr](../../tools/herdr/index.md): terminal multiplexer for agents. One workspace per repo, tabs and panes inside it, a CLI that returns JSON so an agent can create tabs and start, prompt and read sibling agents.
- treehouse (`github.com/kunchenguid/treehouse`): git worktree pool manager. Keeps a pool of ready worktrees per repo under `~/.treehouse/<repo>-<hash>/<N>/<repo>`. A worktree is leased, used, then returned to the pool with its build caches intact instead of being recloned.

## The shape

1. One herdr workspace per repo.
2. Every tab or pane that hosts an agent gets its own treehouse worktree: lease a slot, create the tab with `--cwd` pointing at that worktree, start the agent there.
3. Leases survive with no process inside them, so a slot stays reserved across agent restarts until `treehouse return`.
4. An orchestrating agent in one pane creates tabs, starts sibling agents, prompts them, waits, and reads their output. Fan-out across worktrees is scriptable.

## Procedure

Precondition: run from inside a herdr pane, so `HERDR_ENV=1` plus `HERDR_WORKSPACE_ID`, `HERDR_TAB_ID` and `HERDR_PANE_ID` are set. All `herdr` commands return JSON; parse IDs from the responses.

1. Find the workspace: `herdr workspace list`, then `herdr tab list --workspace <id>` and `herdr pane list --workspace <id>` as needed.
2. Lease a worktree from the repo root, one per agent:
   ```bash
   treehouse get --lease --lease-holder cc-wt1 --json
   ```
   Returns the worktree path. The checkout is detached HEAD at `main`.
3. Create a tab at that path without stealing focus:
   ```bash
   herdr tab create --workspace <id> --cwd <worktree-path> --label wt1 --no-focus
   ```
   Read `result.tab.tab_id` and `result.root_pane.pane_id`.
4. Start the agent in the new pane. This blocks until the agent is ready and moves UI focus to that pane:
   ```bash
   herdr agent start wt1 --kind claude --pane <pane_id>
   ```
5. Prompt, wait, read:
   ```bash
   herdr agent prompt wt1 "<text>" --wait --timeout <ms>
   herdr agent wait wt1 --timeout <ms>
   herdr agent read wt1 --source visible --lines 80     # or --source recent-unwrapped
   ```
6. Check which slots are occupied: `treehouse status` lists the pids living in each slot.
7. Clean up: `herdr tab close <tab_id>` per tab, then `treehouse return --force <worktree-path>` per worktree. `treehouse destroy <pool> --all --yes` removes a pool entirely.

Done when: `herdr agent list` shows no leftover agents, `treehouse status` shows every slot free, and `git status` in the main checkout is clean.

## Gotchas

- Each agent's untracked files land only in its own worktree; the main checkout stays clean. This is the point.
- Worktrees are detached HEAD. An agent must `git switch -c <branch>` before committing.
- Without a `treehouse.toml` or `.worktreeinclude`, gitignored files such as `node_modules` are not seeded into worktrees.
- `herdr agent read` with a larger `--lines` cannot recover output that scrolled off the agent's alternate screen. Ask the agent to write long output to a file instead.
- Slot IDs, pane IDs and agent names are per herdr server. Do not rely on another client's focused pane; use `--current` or explicit IDs.
- `treehouse return --all` from the README does not exist in v2.3.0; return each path.
- `go install github.com/kunchenguid/treehouse@latest` gives v1.8.0 because the module path has no `/v2` suffix, so Go cannot see v2 tags. Install the release binary by hand (see the journal, 2026-09-20).
- A fresh pane's first keystrokes can be eaten by the oh-my-zsh update prompt. Set `zstyle ':omz:update' mode auto` before sourcing oh-my-zsh in `~/.zshrc`.

## Open questions

- How branches flow back from worktrees: a PR per worktree, or merge into the main checkout?
- Which gitignored files to include per repo via `treehouse.toml` or `.worktreeinclude`.
- Whether the `--lease-holder` label should encode the herdr pane or agent name so `treehouse status` and `herdr agent list` can be correlated.

Tried on 2026-09-20 with three Claude Code sessions; see [journal](../journal.md).
