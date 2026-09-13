# Remote VPS setup

Run agent sessions 24/7 on an always-on Linux VPS (Hetzner or any provider), attach from any device. Generic: swap in your own values wherever you see `<placeholder>`. Concepts (what a VPS, SSH, herdr and cloud-init each do) are in [notes/concepts/](../notes/concepts/index.md).

## 1. Provision

- 4 GB RAM minimum (Claude Code's floor). More if other services share the box.
- Note the public IP and SSH login user.

## 2. First connection

```bash
ssh <user>@<vps-ip>
```

Public-facing machine, so: enable unattended security upgrades, and if unrelated services run on the same box, give this workspace its own unprivileged Linux user. See the security section.

## 3. Install and authenticate Claude Code

The normal login opens a browser, which a headless VPS lacks. Pick one:

- On a machine with a working login run `claude setup-token`, then on the VPS:
  ```bash
  export CLAUDE_CODE_OAUTH_TOKEN=<token>
  ```
  Put the export in the profile the persistent session sources, not only the interactive shell.
- Or set `ANTHROPIC_API_KEY` to bill through the API.

## 4. herdr instead of raw SSH

Install herdr, then follow [tools/herdr/setup.md](../tools/herdr/setup.md). From now on every agent starts inside a herdr pane. A process started directly in the SSH shell dies when the connection drops; one started inside herdr keeps running and is there to reattach to.

Reconnect from anywhere: `herdr --remote <host>`, or `ssh` in and run `herdr`.

## 5. Connect GitHub

[tools/gh/index.md](../tools/gh/index.md). Then `gh repo clone <owner>/<repo> ~/<repo>`.

## 6. Per-machine MCP registrations

MCP servers are registered outside the repo, so redo each one on the VPS. Sign-in flows that need a browser either print a URL to open on any device, or wait on a `localhost:<port>` callback. For the callback case, reconnect with a port forward and run the sign-in again:

```bash
ssh -L <port>:localhost:<port> <user>@<vps-ip>
```

## 7. Carry over settings

```bash
scp ~/.claude/settings.json <user>@<vps-ip>:~/.claude/settings.json
```

Then on the VPS delete the `hooks` block (it points at a macOS path) and run `herdr integration install claude` to regenerate it. The `deny`/`ask` rules copy unchanged. Reference: [tools/claude-code/preferences.md](../tools/claude-code/preferences.md).

## 8. Run persistently

```bash
herdr
cd ~/<repo>
claude
```

Detach with `ctrl+b q`. Close the laptop. Reattach later; the session is where you left it.

## Security on a shared VPS

- Dedicated unprivileged Linux user for this workspace, separate from other services and from root.
- Run Claude Code inside a container (Docker/Podman) on top of its own sandbox, so a misled agent cannot reach the host filesystem or other services. Restrict egress to Anthropic's API, GitHub and whatever MCPs need.
- Keep the built-in sandbox on (`/sandbox`); on Linux install `bubblewrap` and `socat`.
- Separate SSH keys and GitHub tokens per workspace. One leak, one blast radius.
- Keep the global `deny` rules; they cost nothing and catch mistakes regardless of sandboxing.
