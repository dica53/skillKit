---
name: principle-encode-lessons-in-structure
description: "Apply when you are about to add a rule to a skill, an agent instruction file, a code comment, or memory, or when you make the same correction a second time. Make a tool enforce the rule instead of writing it down again."
---

# Encode lessons in structure

A written rule works only if someone reads it and remembers it. A tool that enforces the rule works every time. So when the same mistake happens twice, more wording will not fix it. Make the mistake impossible, or make it fail loudly.

For example, reviewers keep asking authors to stop importing from another package's internal files. A note in the contributing guide depends on every author reading it. A lint rule that rejects those imports stops the mistake, and the note is no longer needed.

## How

Use the simplest tool that catches the mistake where it happens:

- **A type or schema:** the wrong value does not compile.
- **A lint rule or CI check:** the mistake fails before merge.
- **A harness hook:** the agent's command is blocked, changed, or queued.
- **A script or a better default:** the right way is also the easy way. For example, a setup script that creates config files, so nobody has to remember to.
- **A runtime check:** the code stops with a clear error message.

When a tool enforces the rule, delete the written rule. If you keep both, readers cannot tell which one is correct.

## When to keep the rule as text

Use a tool only for rules that are true every time. If a rule needs judgment, or people sometimes have a good reason to break it, a tool will block those good reasons too. Keep it as text, put it where people make that decision, and add one real example of the mistake.

## Check

Before you add or repeat a rule, ask: "Can a tool stop this mistake or make it obvious?" If yes, and the rule has no exceptions, build the tool. Do not also keep the text.
