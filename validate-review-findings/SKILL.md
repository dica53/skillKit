---
name: validate-review-findings
description: Validate code review findings and PR comments before acting; reject false positives and push back with evidence. Use when judging findings from any reviewer, human or bot.
---

# Validate review findings

A finding is a claim, not an instruction. Act only on findings that are real, in scope, and worth the change.

## Validate

- Reproduce or trace the claim against the actual code, callers, contracts, and tests; run a focused check when reading is not conclusive.
- Merge duplicates across reviewers and passes.
- Classify each finding as valid, false positive, out of scope (follow-up), or needs a decision from the user.

## Common false positives

- The claim misreads code, or the issue is already handled elsewhere (guard, caller, type, framework).
- The issue is on an unreachable path, or depends on inputs the contract excludes.
- The claim is based on stale diff context or a superseded commit.
- The suggestion is a style preference or a speculative abstraction.
- The suggestion conflicts with repo conventions or an explicit decision made for this task.

## Push back

- Decline with evidence: cite the code, test, or contract that disproves the claim, in one or two sentences.
- Concede quickly when the evidence supports the reviewer; do not defend code out of ownership.
- When a finding is partly right, fix the real part and say what you left out.
- Escalate to the user when the disagreement turns on product intent or a tradeoff you have no authority to settle.
