# New project setup

Bootstrap a repo with agent rules and the default skill set. Read [template/index.md](../template/index.md) first; it explains what each piece is for. Done when the checklist at the end passes.

1. Create `AGENTS.md` from [template/AGENTS.md](../template/AGENTS.md). Keep the communication, commit and skills sections; add project-specific sections below them.
2. Symlink: `ln -s AGENTS.md CLAUDE.md`.
3. Install the default skills:
   ```bash
   npx skills@latest add mattpocock/skills -y
   npx skills@latest add humanlayer/skills --skill show-me -y
   npx skills@latest add ayghri/i-have-adhd -y
   ```
   This writes `.agents/skills/`, `skills-lock.json`, and the `.claude/skills/` symlinks.
4. Create `.gitignore` from [template/.gitignore](../template/.gitignore) and `README.md` from [template/README.md](../template/README.md), then fill in the project specifics.
5. Commit in lowercase multi-line style (rule in `AGENTS.md`).

## Checklist

- `CLAUDE.md -> AGENTS.md`
- `ls .claude/skills` lists `grill-me`, `i-have-adhd`, `show-me` among others
- `skills-lock.json` committed
