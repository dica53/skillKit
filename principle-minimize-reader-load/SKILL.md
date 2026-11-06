---
name: principle-minimize-reader-load
description: "Apply when code is hard to trace, or before adding a wrapper, layer, type, or piece of state. Keep the layers a reader must follow and the hidden state they must remember as small as possible."
---

# Minimize Reader Load

Code is maintainable when a reader can understand it quickly. Two things make that hard:

- **Layers to trace:** wrappers and indirections between a question and its answer.
- **State to hold:** hidden or changing context the reader must keep in their head.

They are separate problems. A flat file full of globals can be as hard to follow as a stack of six adapters. Line counts and "clean architecture" are only proxies for this.

## How

- **Remove layers that cost more than they save:** wrappers with one caller, adapters with one implementation, indirection added "in case". Inline them.
- **Make each layer change the abstraction.** A layer that repeats the same methods and arguments as the one below adds reading without hiding anything.
- **Prefer narrow interfaces that hide real decisions.** A wide interface that hides little makes readers learn both sides.
- **Shrink state:** return values over mutation, locals over fields, fields over module state, and module state over globals. Derive values instead of syncing copies.
- **State an invariant once, at the boundary,** not again in every consumer.

Before adding a layer or a piece of state, ask whether it removes at least as much reading elsewhere.

## Check

Can a new reader answer "where does X come from?" and "what can change X?" in under 30 seconds? If not, cut layers or state.
