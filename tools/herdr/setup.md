# herdr setup

1. Install (single binary, no dependencies): follow https://herdr.dev for the current command. Binary lands in `~/.local/bin/herdr`.
2. Copy [config.toml](config.toml) to `~/.config/herdr/config.toml`. It turns off onboarding, toasts and sounds, uses dot status indicators and the gruvbox theme.
3. Register the Claude Code integration so the sidebar tracks agent state:
   ```bash
   herdr integration install claude
   ```
   This writes a `hooks.SessionStart` entry into `~/.claude/settings.json` pointing at a script under `~/.claude/hooks/`. Run it on every machine; the path is machine-specific.
4. Start or reattach: `herdr`.

## Remote use

Run herdr on the always-on machine, never on the laptop. Attach from anywhere:

```bash
herdr --remote <host>
```

or `ssh` in and run `herdr`. Rename a machine label with `herdr machine list` (note the `profile-id`) then `herdr machine rename <profile-id> --label "<name>"`.

Terminal choice: Ghostty, with no native tabs or splits, so every shortcut reaches herdr. iTerm2 works but its own tabs and keybindings collide with the `ctrl+b` prefix. See [ghostty](../ghostty/index.md).
