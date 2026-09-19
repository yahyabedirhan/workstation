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

## Workflows

Use a workflow when the task crosses a session boundary or combines existing
skills into a repeatable path.

| Workflow | Use when | Entry points |
| --- | --- | --- |
| [Handoff](.workflows/handoff-workflow.md) | Work must continue in another session, or a previous session left `HANDOFF.md` | `/handoff`, `/continue` |
