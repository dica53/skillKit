---
name: principle-boundary-discipline
description: "Apply when wiring validation, error handling, framework adapters, or a component that several surfaces reuse. Check inputs where data enters the system, trust typed data inside it, and keep caller-specific policy at the edge."
---

# Boundary discipline

A boundary is where data enters your code from somewhere you don't control: a request, a config file, an external API, a URL. Check and convert data there, once. Inside, trust the types.

## The pattern

- **At the boundary:** validate input, turn raw data into typed models, and handle errors.
- **Inside:** pass typed data along. Don't check it again.
- **Across the boundary:** expose domain concepts, not the other side's internal shapes. General mechanism lives inside; caller-specific policy lives at the edge.

For example, a reusable chart should take the data it plots as a prop. Each page that uses it decides where that data comes from. The chart should not reach into one page's context and fall back to it.

## In practice

- Parse config and raw payloads into domain types where they arrive, not deep in business logic.
- Don't pass transport, storage, or framework types through your public API.
- Don't repeat null checks deep in a call chain when the boundary already checked.
- Keep business logic in pure functions with no framework dependencies, so you can test it without the framework.

## Checks

- Is this data crossing a boundary right now? If not, more validation is noise.
- Can this logic be a pure function that the framework code just calls? If so, extract it.
- Does this shared component know which caller it serves? If so, move that knowledge to the caller.

Related: `principle-type-system-discipline` for how to type what the boundary produces.
