---
name: skill-writing
description: Write or revise concise agent skills that balance the Bitter Lesson with useful guidance, preferences, and context.
---

# Skill writing

The Bitter Lesson favors general methods that improve with compute, data, and feedback. Give agents durable goals and constraints; leave methods open to adaptation.

Write only what changes behavior today. Use these as questions for deciding what to include, not as sections to fill; many skills need only a purpose and a few principles:

- **Purpose:** desired outcome and when the skill applies.
- **Bar:** the standard that defines acceptable work.
- **Context:** relevant facts, tools, and boundaries the agent cannot reliably infer.
- **Preferences:** defaults, clearly separated from requirements.
- **Checks:** observable success criteria and necessary safety constraints.

When writing skills based on user sessions, don't overfit on specific user tasks. Write durable guidance that captures the essence of expected behavior.

Prefer decision criteria over rigid recipes. Use fixed steps only where deviation risks a concrete failure. Avoid encoding current model weaknesses as permanent rules.

State the principle that generates the cases, not the cases. When you find yourself listing examples (file types, steps, tools, places to look), write the one rule they share instead. Leave out anything a capable agent would do unprompted.

Write each principle as a property of a good result ("reversible", "idempotent"), not as an action to take or a list of things to avoid. Don't add separate sections for checks or steps that the principles already imply.

Most skills fit in a few short principles and under about 150 words. A longer draft usually means you are teaching the method instead of setting the goal.

After drafting, test each line: would a capable agent act differently without it? If not, delete it. Expect the final skill to be a fraction of the first draft.

Remove generic advice, speculative cases, and unnecessary resources. Revise from observed failures; delete guidance as capabilities improve.

## Writing style

- Write as concisely as possible without losing meaning.
- State each idea once; refer to shared guidance instead of duplicating it (`principle-durable-guidance`).
- Use headings for hierarchy, paragraphs to separate ideas, and lists for related points.
- Avoid relative links, which can break when skills are symlinked; prefer skill names or stable references and harness-agnostic guidance where possible.
