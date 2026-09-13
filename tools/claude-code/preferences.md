# Claude Code preferences

Install: `brew install claude` on macOS, `npm install -g @anthropic-ai/claude-code` on Linux. Official docs: https://code.claude.com/docs

## Global settings (`~/.claude/settings.json`)

Reference copy: [settings.json](settings.json). Apply on a new machine by copying it to `~/.claude/settings.json` and replacing `$HOME` with the real home path.

Blocks, ranked by how much it hurts to lose one:

1. `permissions.deny` and `permissions.ask` - safety rails. Identical on every machine. Blocks destructive shell (`rm -rf`, `dd`, `sudo`, `bash -c`), history rewrites (`git push --force`, `git reset --hard`), repo-level `gh` mutations, and reads of `.env`, `secrets/`, `~/.ssh`, `~/.aws`.
2. `enabledPlugins` and `extraKnownMarketplaces` - the `i-have-adhd` plugin comes from the `ayghri/i-have-adhd` marketplace. Missing these means the plugin is silently absent.
3. `hooks.SessionStart` - the herdr sidebar integration. Machine-specific path. Regenerate with `herdr integration install claude` instead of copying (see [herdr](../herdr/index.md)).
4. `model`, `effortLevel` - `opus`, `medium`.
5. `voice`, `theme`, `agentPushNotifEnabled` - cosmetic, skip on a headless machine.

## Project settings (`<repo>/.claude/settings.json`)

Rule: **global = safety rails, project = convenience.**

- Project files hold an `allow` list only. Let it grow from permission prompts as the project is used.
- `deny` and `ask` stay global so no project can loosen them.
- Machine-specific or personal entries go in `.claude/settings.local.json` (gitignored by default).

## Skills

Skills live in `.agents/skills/` and are symlinked into `.claude/skills/`. See [AGENTS.md](../../AGENTS.md) for the symlink rule and [template/](../../template/index.md) for the default skill set.
