# gh

GitHub CLI. Handles account login and SSH key in one step, which is why it replaces manual `ssh-keygen` plus pasting keys.

## Setup on a new machine

1. Install: `brew install gh` (macOS) or `sudo apt install gh -y` (Debian/Ubuntu).
2. `gh auth login`, choose GitHub.com, SSH, let it generate and upload a key. It prints a one-time code and URL; approve on any browser.
3. Set identity:
   ```bash
   git config --global user.name "<name>"
   git config --global user.email "<email>"
   ```
4. Clone: `gh repo clone <owner>/<repo>`.
5. Verify: `ssh -T git@github.com` prints a greeting.

Pick one path for keys: either `gh auth login` generates one, or you run `ssh-keygen -t ed25519` and paste `~/.ssh/id_ed25519.pub` at github.com/settings/keys. Doing both leaves a stray key.

## Guard rails

Global Claude Code settings deny `gh repo delete/edit/archive/rename`, `gh ssh-key`, `gh gpg-key`, and ask before `gh api`, `gh secret`, `gh variable`. See [claude-code](../claude-code/preferences.md).

Docs: https://cli.github.com/manual
