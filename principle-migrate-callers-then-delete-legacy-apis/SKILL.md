---
name: principle-migrate-callers-then-delete-legacy-apis
description: "Apply when introducing a new internal API, prop, or contract while old callers still use the previous one. Move every caller to the new contract and delete the old one in the same change, instead of keeping a compatibility path."
---

# Migrate callers, then delete the legacy API

When you replace an internal API, move every caller to the new one and delete the old one in the same change. Don't keep a fallback "for compatibility": it doubles the paths readers must understand and tends to stay forever.

For example, when a component gains a required prop that replaces reading a context, update every call site to pass the prop. Then remove the context fallback. Don't leave the prop optional with the old behavior as the default.

## How

- Find every caller first, with a search or the type checker. A required parameter makes the compiler list them for you.
- Update tests to check the new contract. Delete tests that only protect the old implementation.

## When this applies

- No external users depend on the old API.
- The codebase can take a coordinated breaking change.
- The new API is part of a simplification or refactor.

If outside users depend on the old API, deprecate it with a clear removal plan instead.
