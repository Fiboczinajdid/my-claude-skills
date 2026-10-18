# my-claude-skills

All Claude skills I've built.

This repo is a personal collection of [Claude Skills](https://www.anthropic.com/news/skills) — reusable instruction files that extend what Claude can do, either in [claude.ai](https://claude.ai) or in [Claude Code](https://claude.com/claude-code).

## Skills in this repo

| Skill | What it does | Trigger |
|---|---|---|
| [`makeprompt`](./makeprompt) | Turns a task description into a ready-to-paste prompt for Claude, tailored to Claude Code, a one-off chat, or Project instructions | `/makeprompt` |
| [`decision-log-message`](./decision-log/decision-log-message) | Logs every judgment call Claude made on its own in one response: assumptions, choices, tradeoffs, with the reason and the alternative | `/decision-log-message` |
| [`decision-log-session`](./decision-log/decision-log-session) | Turns on a decision log for the rest of the conversation, shown only when a response made a Medium or High impact decision | `/decision-log-session` |
| [`training-plan`](./training-plan) | Builds the most optimal, research-based training plan for any goal after a thorough interview, and updates existing plans | `/training-plan` |

The two `decision-log` skills live together in [`decision-log/`](./decision-log), which has its own README.

## Installation

### Claude.ai (web / desktop / mobile)

1. Download the ZIP of the skill you want (don't unzip it):

   | Skill | Download |
   |---|---|
   | `makeprompt` | [makeprompt.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/makeprompt.zip) |
   | `decision-log-message` | [decision-log-message.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/decision-log-message.zip) |
   | `decision-log-session` | [decision-log-session.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/decision-log-session.zip) |
   | `training-plan` | [training-plan.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/training-plan.zip) |

2. Go to **Settings → Customize → Skills**.
3. Upload the ZIP. If a skill with the same name exists, remove the old one first.
4. Make sure it's enabled.

The ZIPs are rebuilt automatically every time this repo changes, so these links always give the latest version. All of them are also listed on the [Skill downloads](https://github.com/Fiboczinajdid/my-claude-skills/releases/tag/skills) release page.

### Claude Code (and other coding agents)

With [`npx skills`](https://github.com/vercel-labs/skills) (needs [Node.js](https://nodejs.org)):

```bash
# Choose skills from a list
npx skills add Fiboczinajdid/my-claude-skills --full-depth

# Or install one skill directly
npx skills add Fiboczinajdid/my-claude-skills --full-depth --skill training-plan
```

`--full-depth` makes the installer also find the skills inside `decision-log/`. Add `-g` to install a skill for all your projects instead of only the current one. Run `npx skills update` later to get newer versions.

Or manually, with git:

```bash
git clone https://github.com/Fiboczinajdid/my-claude-skills.git

# Copy the skill you want
cp -r my-claude-skills/<skill-name> ~/.claude/skills/

# Or symlink, so future updates in this repo flow through automatically
ln -s "$(pwd)/my-claude-skills/<skill-name>" ~/.claude/skills/<skill-name>
```

For skills grouped in a folder (like `decision-log/`), use the path to each skill folder, e.g. `decision-log/decision-log-message`.
<!--
## Adding a new skill to this repo

1. Create a new folder at the repo root, named after the skill (e.g. `my-new-skill/`). The folder name must be unique across the repo, since it becomes the ZIP's name.
2. Add a file named exactly `SKILL.md` inside it with YAML frontmatter (`name`, `description`) followed by the instructions.
3. If the skill needs supporting files (scripts, templates, reference docs), add them alongside `SKILL.md` in the same folder.
4. Add a row for it in the skills table and in the download table above. The download link is `https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/<skill-name>.zip`.
5. Commit and push to `main`. The ZIP is built automatically within a minute or so.
-->
## License

MIT — see [LICENSE](./LICENSE). Feel free to copy, adapt, or reuse any of these skills.
