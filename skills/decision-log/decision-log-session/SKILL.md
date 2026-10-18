---
name: decision-log-session
description: Turn on a decision log for the rest of the conversation, showing Medium and High impact judgment calls in each response. Use only when the user types /decision-log-session; never trigger on your own.
disable-model-invocation: true
---

# Decision log: session

The user typed `/decision-log-session`. From now until it is turned off, track the decisions you make in each response that the user did not explicitly specify, and show a log whenever any of them is Medium or High impact.

Write the log and the on/off confirmations in the language of the conversation.

## Turning it on and off

- On activation, confirm in one line that the session decision log is on (Medium and High impact), then carry on with any task in the same message.
- Turn it off when the user types `/decision-log-session` again, or asks in their own words to stop the logs. Confirm in one line that it is off.
- While it is on, if the user types `/decision-log-message`, that skill takes over for that one response (full log, all impact levels). Resume session behavior afterwards.

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
| High / Med | What you chose | The actual reason | The main option not taken, and when it would be the better pick |

- **Impact** reflects the effect on behavior, security, cost, or maintainability, and how hard the choice is to reverse.
- **Why** must be the real reason. If you went with a default without weighing options, say so. Do not invent a rationale after the fact.

## When and how to show the log

- Show a log in a response only if that response made at least one Medium or High decision. If it made none, show nothing: no log and no "no decisions" line.
- List Medium and High entries, High first. Mark any entry that needs the user's confirmation with ⚠️.
- Hide Low entries. If there were any, end the log with one line saying how many lower-impact decisions were not shown and that the user can ask to see them. If asked, list them.
- Each log covers only the decisions made in that response. If a decision reverses an earlier one, say so in its entry.
- Once the user approves or overrides a decision, treat it as specified and do not log it again.
- Place the log after the output and before any request for approval or next step. Do not put it inside the deliverable itself (code comments, the document) unless the user asks.
- Keep each entry to one or two lines.
