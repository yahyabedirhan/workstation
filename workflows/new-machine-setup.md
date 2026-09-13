# New machine setup

Turn a fresh machine into the standard agent environment. Agent-driven: read each step, run it, adapt paths for macOS vs Linux. Done when the checklist at the end is all green.

1. Install the base tools: `git`, `gh`, `claude`, `herdr`, and on macOS `ghostty`. Per-tool install commands live in [tools/](../tools/index.md).
2. Authenticate Claude Code. Interactive machine: run `claude` and log in. Headless machine: see [remote-vps-setup.md](remote-vps-setup.md) step 3.
3. Apply global Claude Code settings: copy [tools/claude-code/settings.json](../tools/claude-code/settings.json) to `~/.claude/settings.json`, substitute `$HOME`, then delete the `hooks` block. Details in [preferences.md](../tools/claude-code/preferences.md).
4. Install herdr config and integration: [tools/herdr/setup.md](../tools/herdr/setup.md) steps 2 and 3. Step 3 regenerates the `hooks` block deleted above.
5. Connect GitHub: [tools/gh/index.md](../tools/gh/index.md).
6. macOS only: Ghostty config, [tools/ghostty/index.md](../tools/ghostty/index.md).
7. Clone this repo so the machine carries its own documentation:
   ```bash
   gh repo clone yahyabedirhan/workstation ~/workstation
   ```

## Checklist

- `claude` starts and shows the `opus` model
- `~/.claude/settings.json` contains the `deny` list and a `hooks.SessionStart` entry
- `herdr` opens and the sidebar shows a Claude pane's state after starting `claude` inside it
- `ssh -T git@github.com` greets you by username
