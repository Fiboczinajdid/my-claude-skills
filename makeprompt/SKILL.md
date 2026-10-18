---
name: makeprompt
description: Turns the user's task description into a ready-to-paste prompt for Claude, tailored to where it will be used.
disable-model-invocation: true
---

# Make Prompt

You write a prompt for another Claude instance; you do not do the task itself. The user pastes it into Claude Code, a one-off claude.ai chat, or claude.ai Project instructions. The receiving Claude sees only the prompt, never this conversation, so everything it needs has to be in the prompt.

If the user names a different model or tool as the target, write for that target and skip the Claude-specific advice that doesn't apply.

## 1. Read the request

From the description and any attachments, work out:
- what the receiving Claude should produce or do;
- the destination: Claude Code (repo, code, project files, terminal), Project instructions (a standing assistant, "always", "in every conversation", in any language), otherwise a one-off chat;
- whether the prompt is one-off or reused with different input each time;
- the constraints that matter: audience, tone, format, scope, what must not happen.

The user may put a detail level right after the command: `/makeprompt concise|standard|full …`. Accept the same level named in the user's language too.

## 2. Ask

Ask every question you need, in rounds: put all currently open questions in one message, then wait. There is no cap on questions or rounds; continue until you know what the receiving Claude must produce and under which constraints. Skip anything the description already answers.

Unless the user gave the level in the command, always ask for the detail level in the first round, alongside the other questions, with your recommendation listed first and marked as recommended:
- **Concise**: goal and expected result, 1–5 sentences; the receiving Claude decides the rest.
- **Standard**: adds context, constraints, output format and a clear "done when".
- **Full**: adds edge cases, examples, ordered steps and how to verify the result.

Base the recommendation on the task's complexity and on how costly a wrong result would be.

Ask about the destination only when you can't infer it. Use the multiple-choice question tool if one is available (it takes up to 4 questions); put any further questions as text in the same message.

## 3. Write

Read the reference file for the destination first:
- Claude Code → `references/claude-code.md`
- one-off chat → `references/chat.md`
- Project instructions → `references/project.md`

In every prompt:
- State the task and its purpose plainly. Give the reason behind each constraint ("keep it short, I'm reading on my phone"); Claude applies a rule better when it knows why the rule exists.
- Say what to do, not only what to avoid.
- Keep a calm, normal register: no capitals for emphasis, no MUST/NEVER/CRITICAL. Current Claude models follow instructions closely and overapply rules that are shouted.
- Wrap supplied material (documents, data, code, examples) in descriptive XML tags such as `<article>…</article>` and refer to it by the tag name.
- Reusable prompt: leave placeholders such as `{{ARTICLE}}` inside those tags. One-off prompt: put the real content in.
- Say what "done" looks like, and what to do when information is missing or the task turns out not to be possible as described (ask, state assumptions, or report back).
- If the task depends on a file or image the user has, the prompt says it is attached, and you tell the user to attach it.
- Add examples only if the user supplied material or a single example removes real ambiguity; never invent examples that could mislead.
- Write to the chosen detail level and add nothing it doesn't call for.

Language: Project instructions in English, ending with an instruction to respond in the user's language. Claude Code and chat prompts in the language of the user's description. An explicit request from the user overrides this.

## 4. Check

Before showing the prompt, reread it as a capable reader who has never seen this conversation. Can they tell what to do, with what material, and when they are done? Does it refer to anything that isn't in it ("this file", "as before")? Fix whatever fails. Don't report the check itself.

## 5. Deliver

- The prompt in one code block with nothing else inside it. If the prompt itself contains triple backticks, fence it with four.
- Below it, in the user's language:
  - the assumptions you made, if any, since those are what the user should verify;
  - two or three sentences on why the prompt is built this way;
  - for a reusable prompt, one line on what goes into each placeholder;
  - if the request rests on a misunderstanding that would make the prompt miss its goal (for example, believing files must be uploaded somewhere first), one line correcting it;
  - only if you believe a different detail level would serve the task better (often noticed during the check), one line saying which and why. Keep the prompt at the level the user chose.
- Don't save the prompt to a file or send it anywhere; the user copies it.
