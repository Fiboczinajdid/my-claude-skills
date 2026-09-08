---
name: makeprompt
description: Turns the user's own description of a task into a polished, ready-to-use prompt for another text-based AI/LLM (primarily Claude, but usable for any chat model). Trigger this ONLY when the user's message starts with or explicitly contains the exact command "/makeprompt". Do not trigger on natural-language requests like "write me a prompt" or "make a prompt for AI" without the literal "/makeprompt" command present — wait for the explicit command instead. Do not use this for image, video, or audio generation prompts — this skill is for text/chat models only.
---

# Make Prompt

This skill converts a rough idea, task description, or goal — however short or detailed — into a well-structured prompt the user can copy and paste into another AI chat (most often Claude, but the output should work reasonably well with other LLMs too).

The deliverable is **the prompt itself**, not a completion of the underlying task. Don't do the task described in the user's input — write a prompt that would get an AI to do it well.

## Step 0 — Always ask about desired length

Before drafting, always ask the user how long/detailed they want the final prompt to be (e.g. short and to-the-point vs. more thorough/structured). Ask this every time, regardless of how detailed their task description already is — it's a standing preference check, not a context gap. This can be combined with any other clarifying questions from Step 1 into one round if both are needed.

## Step 1 — Check if there's enough to work with

Before writing anything, judge whether the user's description gives you enough to produce a genuinely useful prompt. A description is "enough" when you can tell:
- What the AI receiving the prompt is actually supposed to produce (an email? code? analysis? a story?)
- Roughly what context or constraints matter (audience, tone, length, format, must-avoids)

If the description is vague or one-line (e.g. "write me a prompt for writing emails"), **ask as many clarifying questions as needed to fully understand the context** before generating the prompt — there's no cap on how many. Don't guess silently. Keep gathering context until you genuinely know what the receiving AI should produce and what constraints matter; it's fine to go through multiple rounds of questions if the first round's answers open up new ambiguity. Use `ask_user_input_v0` if available so the user can tap instead of type; otherwise ask inline.

If the description is already detailed enough to act on, skip straight to Step 2 — don't add friction by asking questions whose answers are already implied.

## Step 2 — Write the prompt

Draft a prompt that follows solid general prompting practice, adapted to how substantial the task is:

- **State the task clearly and specifically** — what the receiving AI should do, for whom, and why, in plain direct language.
- **Give relevant context** the user provided (audience, constraints, background, examples, tone, format).
- **Specify the desired output format** when it matters (length, structure, sections, code vs. prose, etc.).
- **Include examples** in the prompt only if the user gave you something to work from, or if the task is the kind where one clarifying example genuinely helps (don't invent fake examples that could mislead).
- **Keep it as short as it can be while still being clear.** A two-sentence task doesn't need a ten-section prompt. Scale the prompt's length and structure to the complexity of what's being asked — simple asks get simple prompts, complex or multi-part asks can use light structure (e.g. short labeled sections) to stay unambiguous.
- Write the prompt in the same language the user described their task in, unless they specify otherwise.

## Step 3 — Present it

Show the finished prompt in a copyable code block (triple backticks), with nothing else inside the block — just the prompt text itself, ready to paste elsewhere. After the block, you can add one short line noting any assumptions you made (if you didn't ask clarifying questions but had to infer something minor), but keep this brief — the prompt is the deliverable, not a discussion of it.

Do not save this as a file and do not send it anywhere — it's for the user to copy themselves.

## Examples of good scoping

- User: "/makeprompt pomóż mi z promptem do podsumowywania długich artykułów naukowych" → task is clear enough on content, but still ask about desired prompt length (Step 0), and maybe one more clarifying question about audience if it seems important.
- User: "/makeprompt zrób mi prompt" (nothing else) → too vague, ask what the prompt should help the receiving AI do — and combine with the length question in the same round.
- User: "/makeprompt chcę prompt dla Claude, który pomoże mi pisać cotygodniowe raporty statusu projektu dla mojego zespołu — mam listę zadań z Jiry, chcę żeby AI grupowało je wg priorytetu i pisało krótkie podsumowanie po polsku" → task itself is fully detailed, but still ask the length question (Step 0) before drafting.
