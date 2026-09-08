# my-claude-skills

All Claude skills I've built.

This repo is a personal collection of [Claude Skills](https://www.anthropic.com/news/skills) — reusable instruction files that extend what Claude can do, either in [claude.ai](https://claude.ai) or in [Claude Code](https://claude.com/claude-code).

## Skills in this repo

| Skill | What it does | Trigger |
|---|---|---|
| [`makeprompt`](./makeprompt) | Turns a task description into a polished, ready-to-use prompt for another AI/LLM | `/makeprompt` |

## Installation

### Claude.ai (web / desktop / mobile)

1. Open the skill's folder in this repo and download its `SKILL.md`.
2. Go to **Settings → Customize → Skills**.
3. Upload the file.
4. Make sure it's enabled.

### Claude Code

```bash
git clone https://github.com/Fiboczinajdid/my-claude-skills.git

# Copy the skill you want
cp -r my-claude-skills/<skill-name> ~/.claude/skills/

# Or symlink, so future updates in this repo flow through automatically
ln -s "$(pwd)/my-claude-skills/<skill-name>" ~/.claude/skills/<skill-name>
```

## Adding a new skill to this repo

1. Create a new folder at the repo root, named after the skill (e.g. `my-new-skill/`).
2. Add a `SKILL.md` inside it with YAML frontmatter (`name`, `description`) followed by the instructions.
3. If the skill needs supporting files (scripts, templates, reference docs), add them alongside `SKILL.md` in the same folder.
4. Add a row for it in the table above.
5. Commit and push.

## License

MIT — see [LICENSE](./LICENSE). Feel free to copy, adapt, or reuse any of these skills.
