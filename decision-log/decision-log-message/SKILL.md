---
name: decision-log-message
description: Show a full log of the judgment calls made in this one response. Use only when the user types /decision-log-message; never trigger on your own.
disable-model-invocation: true
---

# Decision log: message

The user typed `/decision-log-message`. Log every non-trivial decision you make in this response that the user did not explicitly specify, and present the log with your output. Earlier messages are context only; decisions made in earlier responses are not part of this log.

Write the log in the language of the conversation.

## What counts as a decision

Log it if it is any of these:
- **Interpretation**: how you read an ambiguous or incomplete instruction
- **Assumption**: something you treated as true without verifying it (data format, environment, audience, scale, versions)
- **Technical choice**: library, architecture, algorithm, data model, file format, tool
- **Tradeoff**: where you favored one quality over another (speed vs. accuracy, simplicity vs. flexibility, cost vs. performance)
- **Scope**: something you added, left out, or deferred

Skip it if:
- the user specified it, or it follows directly from what they specified
- it follows a convention already established in their code, docs or project (log it only if you deviated)
- it is purely stylistic (naming, formatting, wording) and does not affect behavior, security, cost, or maintainability

Test for borderline cases: would the user plausibly have chosen differently, or would it be costly to change later? If either is yes, log it.

## Ask first instead of logging

The log is for decisions that are cheap to revisit. Stop and ask before acting when a decision:
- is hard or impossible to undo (deleting data, sending messages, migrations, purchases, publishing)
- has security, legal, or significant cost implications
- would materially change what the user gets, and the request supports more than one reasonable reading

If the user is not available to answer, take the most conservative option and flag it at the top of the log.

## Entry format

| Impact | Decision | Why | Alternative |
|---|---|---|---|
| High / Med / Low | What you chose | The actual reason | The main option not taken, and when it would be the better pick |

- **Impact** reflects the effect on behavior, security, cost, or maintainability, and how hard the choice is to reverse.
- **Why** must be the real reason. If you went with a default without weighing options, say so. Do not invent a rationale after the fact.

## Presenting the log

- Place it after the output and before any request for approval or next step. Do not put it inside the deliverable itself (code comments, the document) unless the user asks.
- Include all impact levels, ordered High first. Mark any entry that needs the user's confirmation with ⚠️.
- Keep each entry to one or two lines. If there are more than about 10, show High and Medium in full and list Low entries in a single line.
- If there were no unspecified decisions worth logging, say so in one line rather than omitting the log.

## Command without a task

If the message contains `/decision-log-message` but no new task (for example, the user asks what you assumed), log the decisions from your previous response instead. Your reasoning from that turn may no longer be available, only its output, so:
- infer the decisions and their reasons from that output and the conversation
- head the log with "(inferred from the previous response)"
- mark each reason you are inferring rather than recalling with "(inferred)", and never present an inferred reason as the actual one
