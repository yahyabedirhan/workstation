# workstation

Live documentation of my development environment: the tools I use, how they are configured, how I run and manage coding agents locally and on a remote machine, and the rules every other project inherits. Written so an agent can read it and set up a new machine or project.

Public repo. No secrets, usernames, home paths, emails or IPs; a gitleaks pre-commit hook and GitHub Action enforce that.

## Map

- [AGENTS.md](AGENTS.md) - rules for agents working in this repo (`CLAUDE.md` links here)
- [tools/](tools/index.md) - per-tool config and preferences: claude-code, herdr, ghostty, gh
- [workflows/](workflows/index.md) - new machine, remote VPS, new project
- [template/](template/index.md) - reference files and the default skill set for new projects
- [notes/](notes/index.md) - journal and concept explainers
- `.agents/skills/` - installed skills, pinned in `skills-lock.json`

## Start here

- Fresh machine: [workflows/new-machine-setup.md](workflows/new-machine-setup.md)
- New repo: [workflows/new-project-setup.md](workflows/new-project-setup.md)
- After cloning this repo: `./scripts/install-hooks.sh`
