# training-plan

A Claude skill that builds the most optimal, research-based training plan for any person and any goal, after a thorough interview. It gather all important data and also updates an existing plan. It replies in the language you write in.

## What it does

Invoke it with `/training-plan`. It's not a set of plan templates but a process: **collect data → find research → build the plan**.

1. **Asks one question up front**: how much explanation you want with the plan (none / short / detailed).
2. **Lets you tell everything first**: your goal, how you train now, what gets in the way. You can paste or describe your current plan (a photo or a note works too).
3. **Interprets the goal**: breaks any goal, including combined or unusual ones (e.g. bigger arms + higher vertical jump), into motor qualities (strength, power, hypertrophy, endurance, mobility, movement control), sets a main goal and secondary goals, checks for conflicts between them, and asks you to confirm.
4. **Asks only what changes the plan**, in batches of 3–5, from a core set plus modules for each motor quality. For unusual or sport-specific goals it looks up how specialists assess that quality and asks extra questions. Every question can be skipped: a skipped answer is treated as "no data", never filled in with a made-up default. If you skip something key, it asks once at the end whether you're sure. It always asks how many days a week you actually train and your **session budget**: time per session, max sets or max exercises per session (your choice), which becomes a hard limit for every session.
5. **Estimates your strength**: from your weight × reps (Epley/Brzycki, sets up to ~10 reps) or, if you skip that, from proxy questions. Weights are given as ranges, rounded to real plate increments.
6. **Researches before planning**: separate searches per variable (volume, intensity, frequency, exercise selection, rest, order, interference), in English, with a source hierarchy (meta-analyses → ACSM/NSCA position stands → single studies → blogs only with a note). It writes a "research → decision" note for each variable and runs a checklist before handing the plan over. If web search is off, it says so at the start instead of planning from memory.
7. **Delivers the plan** (usually 6–8 weeks) as tables in the chat: exercise, sets, reps, weight, rest, notes. No RPE or reps-in-reserve. Plus the estimated session length, a **weekly sets per muscle** table (every major muscle group trained at least 2 days a week, about 10 weekly sets, with any shortfall named and trade-offs offered), how the plan changes week to week, when to change it, the explanation you chose, and 2–5 sources.

When you come back to change the plan for a specific reason (stalled lift, weights that don't fit, fatigue, pain, a new schedule or goal), it follows the same research process and changes only what it considers necessary. When you want to refresh a plan you've followed for a long time, it first diagnoses what actually stalled, checking the cheap causes (recovery, effort, weekly sets, fatigue) before swapping exercises, keeps what still works and rotates accessories on purpose.

It covers training only, no diet. It asks about injuries to choose exercises, not as a medical screening; if you mention a serious condition, it suggests checking the plan with a doctor or physiotherapist and still builds it.

It only triggers on the explicit `/training-plan` command (`disable-model-invocation: true`).

## Legal boring stuff ehhhh
This skill generates general training suggestions, not medical advice. Train at your own risk, and check with a doctor or physiotherapist before starting if you have an injury, a health condition, or haven’t exercised in a while.

## Files

```
training-plan/
├── SKILL.md                  # main instructions: interview, goal interpretation, research, plan format
└── references/
    ├── data-by-goal.md       # what data to collect per goal and what each item changes
    ├── change-plan.md        # how to change a plan for a specific reason
    └── refresh-plan.md       # how to refresh a plan you've followed for a long time
```

`change-plan.md` and `refresh-plan.md` are read only when you come back with a plan, so building a new plan doesn't load them.
