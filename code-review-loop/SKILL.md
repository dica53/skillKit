---
name: code-review-loop
description: Review changes, fix validated findings, and repeat until no actionable findings remain within scope. Use when review includes taking action.
---

# Code Review Loop

Use the `review` skill for each review pass.

## Act and repeat

- Validate findings with the `validate-review-findings` skill, then fix valid ones within the task's scope and authorization; verify the affected behavior.
- Review the revised diff and repeat until no actionable in-scope findings remain. When the reviewers are on a PR, `babysit` owns the wait between passes and the thread replies.
- If blocked or further passes cannot make progress, report unresolved findings and what would unblock them. Request decisions only for actions beyond existing authority.

## Audit trail

When the change has a PR, keep one PR comment as the record of local review passes, edited in place after every pass:

- **Every pass is listed:** reviewer, focus, and result, newest first.
- **Every finding has an outcome:** fixed (with the commit), declined (with the evidence), moved to a follow-up (linked), or found but older than the change.
- **Latest first:** the newest pass is expanded; earlier passes are collapsed.
- **Review only:** verification evidence stays in the PR description.

## Result

Summarize findings, fixes or reasons for deferral, and verification. List any decisions needed from the user; do not describe an incomplete loop as clean.
