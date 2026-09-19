# template

Reference files for a new project. Read this file before using them. The files are examples to adapt, not a scaffold to copy blindly; the procedure is [workflows/new-project-setup.md](../workflows/new-project-setup.md).

- [AGENTS.md](AGENTS.md) - baseline agent rules: communication style, commit format, skill symlink convention, handoff workflow discovery
- [.gitignore](.gitignore) - baseline ignores for a repo that carries agent skills
- [README.md](README.md) - skeleton with the sections every project README needs

## Why it is built this way

- `AGENTS.md` is the single rules file; `CLAUDE.md` is a symlink to it so Claude Code and every other agent read the same text.
- Skills are a dependency, treated like `node_modules`: `skills-lock.json` pins them, `npx skills add` reinstalls them. Skills written for the project itself also live in `.agents/skills/` and are committed.
- `.claude/skills/` holds symlinks only, so one folder is the source of truth.

## Default skill set

Every project gets:

- everything in `mattpocock/skills` (grilling, research, tdd, code-review, writing-for-agents, and the rest)
- `show-me` from `humanlayer/skills`
- `i-have-adhd` from `ayghri/i-have-adhd`
- the workstation-owned `continue` skill and handoff workflow

Install commands are in the workflow.
