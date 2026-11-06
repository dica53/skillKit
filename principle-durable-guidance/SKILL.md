---
name: principle-durable-guidance
description: "Apply when writing or editing text that outlives the task: code comments, docstrings, READMEs, docs, skills, agent instruction files, or memory. Write the lasting principle once, at the source of truth, and point to facts instead of copying them, so the text does not drift from the code."
---

# Durable guidance

Text drifts when it restates something that changes somewhere else. Code, config, and schemas get updated; prose that copies them does not, and readers cannot tell which one is right. Durable text says what the code cannot say, and points to the code for the rest.

## How

- **Write the why.** Comments, docs, and skills explain intent, constraints, and trade-offs. Leave out what a reader can verify by reading the code: what a function does, its arguments, its call order.
- **One owner per fact.** Each fact lives in one place: code, a schema, config, or a single skill. Other places name that place with a stable reference, such as a skill name, a symbol, a command, or a file. Don't use line numbers or values copied from it.
- **Point to values that drift.** Counts, thresholds, paths, flag names, versions, and IDs belong in the source. Say how to find them ("read the route's settings") instead of stating them.
- **Describe the steady state, not a moment.** Leave out what is true only now: "currently", "new", "recently", "for now". When something really is temporary, state the condition that ends it ("remove once every caller uses X"), not a date or a status.
- **Write the principle, not the incident.** State the rule broadly enough to cover related cases beyond the example that prompted it. Keep one real example if it makes the rule clearer.
- **Indexes and decision logs, not copies.** READMEs and instruction files map where things live and record why decisions were made. They do not repeat what the code currently does.
- **Remove what goes stale.** When you change code, update or delete the text that refers to it. When a tool now enforces a rule, delete the written rule (`principle-encode-lessons-in-structure`).

## Check

- Would renaming a function, changing a value, or moving a file make any sentence false? Would the passage of time? If so, replace the copy with a pointer, or move the dated fact to where history belongs.
- Does any other file already say this? If so, keep one copy and link to it from the other places.
- After a code change, search for comments, docs, and skills that name what changed, and fix them in the same change.
