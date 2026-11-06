---
name: principle-type-system-discipline
description: "Apply when designing types or props, reviewing a function or component signature, or writing statically typed code. Make impossible states fail to compile, give same-shaped values distinct types, parse external data at the boundary, and derive types from the schema that owns them."
---

# Type system discipline

Let the compiler reject impossible states, mixed-up values, and unhandled cases. Prefer designing a special case out of the type over handling it in code.

- **Make impossible states unrepresentable.** If a value can only be "a thing" or "nothing yet", type it as `Thing | null`, not as an optional prop where missing and `null` mean different things. A required prop turns a forgotten value into a compile error instead of a silent blank.
- **Give same-shaped values distinct types.** A `UserId` and an `OrderId` are both strings, but they should not be interchangeable. Use a branded type (or a newtype in other languages). Validate once when you create the value, then trust the type.
- **Treat external data as untyped until parsed.** API payloads, JSON, URL and CLI arguments, environment variables, and database rows need a parse step at the boundary that turns them into the typed model. `principle-boundary-discipline` covers where that step goes.
- **Derive types from the source that owns the shape.** When an OpenAPI spec, GraphQL or protobuf schema, database migration, or design-token file defines a shape, generate or derive the type from it. Don't hand-write a parallel copy that can drift.
