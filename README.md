# workstation

This is where I keep track of how my development environment is set up: the tools I use, how I configure them, how I run coding agents on my laptop and on a remote server, and the rules and skills I want every new project to start with.

It is written so that an agent can read it and set up a new machine or a new repo without me explaining things again. It is also where I write down why I chose things the way I did, so future me can remember.

## What is in here

- [AGENTS.md](AGENTS.md) is the rules file for agents working in this repo. `CLAUDE.md` points to it.
- [tools/](tools/index.md) has one folder per tool with its config and my preferences: Claude Code, herdr, Ghostty, gh.
- [workflows/](workflows/index.md) has step by step procedures that cross several tools: setting up a new machine, running agents on a remote VPS, bootstrapping a new project, handing work off between sessions.
- [template/](template/index.md) has the reference files and the default skill set a new project starts from.
- [notes/](notes/index.md) has a journal with one section per day and explainers for concepts I keep looking up.
- `.agents/skills/` holds the installed skills, pinned in `skills-lock.json`.

## Where to start

- Setting up a fresh machine: [workflows/new-machine-setup.md](workflows/new-machine-setup.md)
- Starting a new repo: [workflows/new-project-setup.md](workflows/new-project-setup.md)
- Just cloned this repo: run `./scripts/install-hooks.sh` once
