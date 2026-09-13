# AGENTS.md

## Communication Style

- Do not overuse the em dash character (—) anywhere.

## Git And Commits

Use lowercase multi-line commit messages:

```text
commit message

- explanation 1
- explanation 2
- explanation 3
```

## Skills

### Adding New Skills

Create the skill under `.agents/skills/<skill-name>/SKILL.md`, then add a symlink so Claude Code picks it up automatically:

```bash
ln -s ../../.agents/skills/<skill-name> .claude/skills/<skill-name>
```

Stage the symlink with `git add .claude/skills/<skill-name>` (not the file inside it).

## This Repo

Public. Every file is read by agents setting up other machines and projects.

- Secrets, usernames, home paths, emails and IPs stay out. Write `$HOME`, `<user>`, `<vps-ip>`. The gitleaks pre-commit hook (`./scripts/install-hooks.sh`) blocks the rest.
- Every folder has a lowercase `index.md` that only points at its files. Content lives in the other files.
- Write for an agent: lead with the action, number the steps, end each procedure with a checkable completion state. Reasoning behind a choice goes in the tool's own doc or [notes/journal.md](notes/journal.md), one section per day.
- Layout: [tools/](tools/index.md) per-tool config, [workflows/](workflows/index.md) cross-tool procedures, [template/](template/index.md) new-project reference, [notes/](notes/index.md) journal and concepts.
