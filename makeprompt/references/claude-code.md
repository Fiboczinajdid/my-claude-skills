# Prompts for Claude Code

Claude Code works inside the user's project folder with access to files, the shell and git. It can read the code itself, so the prompt points it at the work instead of describing code from memory.

- Open with the goal and why it matters to the user.
- Have it explore the relevant parts of the project before changing anything. Name files or folders only when the user named them; guessed paths send it the wrong way.
- For larger or risky changes, ask for a plan first and to wait for approval before editing.
- Scope: what it may change, what it leaves alone (data, config, credentials, public interfaces), and whether it may install packages, commit or push.
- "Done when" should be checkable: tests pass, the app starts, a command gives a specific result. If there are no tests, say how to verify.
- If the project probably holds API keys, `.env` files or other credentials (anything touching exchanges, payments, external accounts), tell it not to print, copy or commit them.
- For "understand this project" tasks: ask for a summary back and for the lasting knowledge (what the project does, how to run it, structure, conventions) to be written into `CLAUDE.md`. That file loads in every future session, so it should stay concise.
- End by asking for a short report: what changed, what was verified, what is left open.

By detail level:
- Zwięzły: goal + done when.
- Standard: + scope, constraints, verification.
- Pełny: + plan first, ordered steps, edge cases, how to roll back.
