---
name: deep-review
description: "Run deep-correctness-review and deep-maintainability-review as parallel subagents, then synthesize their findings. Use for a combined correctness, security and code-quality audit of a branch (formerly thermos)."
---

# Deep review

Run `deep-correctness-review` and `deep-maintainability-review` as async background subagents in parallel, then synthesize their results.

## Workflow

1. Determine the review scope from the user request, PR, current branch, or relevant changed files.
2. Gather the diff and any file/context excerpts needed for reviewers to evaluate the change without guessing.
3. Pass each subagent the same scoped diff/file context and ask it to return prioritized findings with file references and evidence.
4. After both finish, synthesize the results with findings first, deduplicated across reviewers. Weight overlapping findings more heavily, resolve disagreements with your own judgment, and keep summaries brief.

If individual background summaries are already visible to the user, do not restate them wholesale. Surface the unified verdict, the highest-signal findings, and any remaining uncertainty.
