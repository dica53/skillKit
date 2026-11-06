---
name: human-pr-descriptions
description: "Human PR descriptions (visual outline): links, why, special things to note, why it's safe, and a compact change outline. Use when writing or updating the description of any GitHub pull request, in any repository."
metadata:
  user-invocable: false
---

# PR descriptions: why, what to note, why it's safe, visual change outline

Applies to every GitHub PR opened or updated, in any repository, including promotion and stacked PRs.

Goal: a reviewer understands why the change exists and the shape of the implementation without reading long prose. Description content minimizes reader cognitive load. Read the full diff and enough surrounding code before writing. Prose is digestible and visuals are preferred over text explainers.

## Template

Use these parts, in this order, if applicable. Do not add sections beyond them, except where the repository's PR template or rules require them.

```markdown
[TICKET-123](ticket url) | [other relevant link(s)](url)

## Why the change

One sentence: the problem this PR solves and what becomes possible after it ships.

## Special things to note

- 1-3 bullets: reviewer warnings, migrations, compatibility constraints, deliberate omissions, surprising decisions, or a merge/gate order (numbered steps) when one is genuinely needed. Write "- None." if there are none.

## Why it's safe

- 1-3 bullets: what keeps this from breaking existing behavior (unchanged paths, tests, flags, rollout/gate order).

## Change outline

Short sentence, then the view it introduces. Repeat only for the views that help.
```

- Link header: ticket, pre-PR review(s), related plans/docs. Omit the line if there are no links.
- Still follow the repository's PR template headings if it has one; put these parts under it.
- If a repository-specific rule requires an extra field, add that one line, nothing more.

## Change outline: views

Pick the smallest combination that explains the implementation, ordered however tells the story best. Include a view only when it shows something the reviewer cannot already see, omit views that did not change, and name each by what it shows.

- Before/after screenshots for a visual change; After only if there was no prior UI; drawings/captions if noisy; no markup, class, or style diffs.
- SQL tables and endpoint request/response contracts; pseudocode for business logic.
- Key data structures / types.
- Shallow file tree with each changed file's responsibility.
- React component tree, including hooks, state, and package boundaries that matter. Beside screenshots, only for structure they do not show.
- Call tree, call stack, control flow, or data flow (a Mermaid `sequenceDiagram` is fine; GitHub renders it).
- `diff` block when that shape already exists.
- Full shape in a language or `text` block when most of it is new, or diff notation would hide ownership or order.
- Flow diagram for architecture or a path across services.

```markdown
## Change outline

### Before

[screenshot(s)]

### After

[screenshot(s)]
```

Examples:

```diff
 submitForm
   createSession
     persistPrompt
+    expandSkillMention
     launchAgent
```

```diff
 src/
 ├── commands/
+│   └── show-me.ts       # expands the slash command
-└── transport.ts
+└── transport/
+    ├── client.ts
+    └── stream.ts
```

```diff
 on(save)
-  write content
+  if content is unchanged
+    return cached result
+  write new content
```

```tsx
<SessionPage> (apps/example/src/routes/session.tsx)
  useSessionEvents()
  <SessionToolbar>
    <RunSkillButton> (packages/ui)
```

## Style

- Write as one engineer to another: plain, concise, no jargon or slang.
- No per-file diff narration, no restating code obvious from the diff, no walls of text.
- Keep each view to the calls, files, props, states, and boundaries a reviewer needs.
- Leave out load-test caveats, review history, and process notes unless they change how the reviewer should act.
