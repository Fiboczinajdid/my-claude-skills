# decision-log

Two Claude skills that show you the judgment calls Claude made on its own: assumptions, interpretations of vague instructions, technical choices, tradeoffs and scope changes you never asked for. You see them next to the output, before you approve anything.

| Skill | Scope | Trigger |
|---|---|---|
| [`decision-log-message`](./decision-log-message) | One response, full log | `/decision-log-message` |
| [`decision-log-session`](./decision-log-session) | Rest of the conversation, Medium and High impact only | `/decision-log-session` |

Both run **only** when you type the command (`disable-model-invocation: true`). They never switch on by themselves, so they cost nothing in conversations where you don't use them.

## decision-log-message

Type the command together with your task:

```
/decision-log-message build a script that renames these photos by date
```

Claude does the task, then adds a log of every non-trivial decision it made **in that response**: Low, Medium and High impact, highest first. Earlier messages count as context only; their decisions aren't included. If there was nothing worth logging, you get one line saying so.

Typed on its own, without a task (e.g. `/decision-log-message what did you assume?`), it logs the decisions from Claude's **previous** response instead. Claude's reasoning from that turn usually isn't available anymore, only its output, so the log is headed "inferred from the previous response" and inferred reasons are marked "(inferred)".

## decision-log-session

```
/decision-log-session
```

Turns on a log for the rest of the conversation. From then on:

- A response gets a log **only if** it made at least one Medium or High impact decision. Otherwise there's no log at all, not even a "no decisions" line.
- Low impact decisions are hidden. A one-line footer says how many were skipped; ask and Claude lists them.
- Each log covers only that response. Reversed decisions are marked as such, and decisions you've already approved or overridden aren't logged again.
- Type `/decision-log-session` again, or just ask Claude to stop the logs, to turn it off.
- Using `/decision-log-message` while the session log is on gives you the full log (including Low) for that one response, then the session mode resumes.

## What both skills share

**What gets logged.** Interpretations, assumptions, technical choices, tradeoffs and scope changes the user didn't specify. Skipped: things you specified, things that follow your project's existing conventions (unless Claude deviated), and purely stylistic choices that don't affect behavior, security, cost or maintainability.

**Log format.** A table with Impact, Decision, Why and Alternative (plus when the alternative would be the better pick). Entries needing your confirmation are marked ⚠️. "Why" must be the actual reason; if Claude just went with a default, it says so instead of inventing a rationale.

**Ask first.** While either skill is active, Claude stops and asks *before* acting on anything irreversible (deleting data, sending messages, migrations, purchases, publishing), anything with security, legal or significant cost implications, or a request that could reasonably be read more than one way and would change the result.

**Language.** The log is written in the language of the conversation, even though the skills themselves are in English.

## Installation

These are two separate skills in one folder, so install each skill folder on its own, not the `decision-log` folder.

**Claude.ai:** download [decision-log-message.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/decision-log-message.zip) and [decision-log-session.zip](https://github.com/Fiboczinajdid/my-claude-skills/releases/download/skills/decision-log-session.zip), then upload both under **Settings → Customize → Skills**.

**Claude Code:**

```bash
npx skills add Fiboczinajdid/my-claude-skills --skill decision-log-message decision-log-session
```

Or copy them manually from a clone of this repo:

```bash
cp -r my-claude-skills/skills/decision-log/decision-log-message ~/.claude/skills/
cp -r my-claude-skills/skills/decision-log/decision-log-session ~/.claude/skills/
```

## Files

```
decision-log/
├── README.md
├── decision-log-message/
│   └── SKILL.md
└── decision-log-session/
    └── SKILL.md
```
