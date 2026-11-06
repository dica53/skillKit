---
name: principle-model-the-domain
description: "Apply when writing stateful logic, or when code branches a lot or repeats the same assumption about a data shape across files. Encode the domain in a data structure with one owner instead of scattering it across conditionals."
---

# Model the domain

Put the real rules of the domain into a data structure instead of spreading them across `if` statements. The right structure makes invalid states impossible and deletes branches. It is cheap to choose when you write the code and expensive to recover later.

## Reach for

- A state machine instead of several booleans or phase flags that must agree.
- A typed model instead of loose parameters or the same shape assumption repeated in many places.
- A map, registry, lookup table, or discriminated union instead of branching spread across files.
- A reducer or command/event model instead of ad hoc state changes.
- One module that owns one body of domain knowledge, such as "which configured row a hostname maps to". When a second place needs that answer, pass the owner's result along instead of copying its rule.
- A queue, cache, index, tree, or normalized collection when the access pattern calls for it.

If nothing fits, work out what the code must never allow and how the data is read, then pick the structure that encodes exactly that.

## Don't overdo it

Keep boring code when the current shape is clear, local, and unlikely to grow. Be wary of an abstraction that adds a layer without removing branches, duplicated rules, invalid states, or lifecycle risk.

## Signs you skipped this

- A new feature adds one more branch to an existing `if`/`else` chain.
- A second boolean must stay in sync with the first.
- A rule is copied from the module that owns it, with a comment saying so.
- Modules are named after steps (load, validate, save) and repeat the same rules in each step.
