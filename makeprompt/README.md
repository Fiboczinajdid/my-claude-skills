# makeprompt

A Claude skill that turns a rough task description into a ready-to-paste prompt for Claude, built for where you'll use it: Claude Code, a one-off claude.ai chat, or Project instructions.

## What it does

Invoke it with `/makeprompt`, optionally with a detail level: `/makeprompt zwięzły|standard|pełny …`. Then:

1. **Reads your request**: what Claude should produce, where the prompt will be used, whether it's one-off or reusable, and which constraints matter.
2. **Asks what it needs to know**, in rounds, with no cap on questions. It always asks for the detail level (unless you gave it in the command), with a recommendation:
   - **Zwięzły**: goal and expected result, 1–5 sentences.
   - **Standard**: adds context, constraints, output format and a clear "done when".
   - **Pełny**: adds edge cases, examples, ordered steps and verification.
3. **Writes the prompt** using Claude-specific practice (XML tags for material, reasons behind constraints, calm wording without shouted rules, a clear finish line) plus destination-specific notes from `references/`.
4. **Checks it** as a reader who has never seen your conversation, and fixes gaps.
5. **Delivers** the prompt in a copyable code block, followed by assumptions to verify, a short "why it's built this way", and a suggestion for a different detail level only when it's warranted.

It only triggers on the explicit `/makeprompt` command (`disable-model-invocation: true`), so its description doesn't take up context in other conversations.

## When to use

It's primarly made for making prompts on fresh sessions, when you dont want to type sophisticated prompts. This skill makes your prompt easier for AI to understand and eliminates possible
ambiguities. Performs the best in easy and simple tasks

## Files

```
makeprompt/
├── SKILL.md                  # main instructions
└── references/
    ├── claude-code.md        # prompts for Claude Code
    ├── chat.md               # prompts for a one-off chat
    └── projekt.md            # Project instructions
```

Only the reference file for the chosen destination is loaded, which keeps each run cheaper.
