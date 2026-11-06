---
name: principle-redesign-from-first-principles
description: "Apply when a new requirement, caller, or surface has to fit into an existing design. Redesign as if the requirement had been there from the start instead of bolting on a special case."
---

# Redesign from first principles

When a change has to fit an existing design, don't bolt it on. Ask what you would build if the new requirement had been part of the original brief, and build toward that.

For example, when a second page needs a component that so far read one page's context, the question is not "how do I add a second input path?" It is "what input would this component take if both pages had existed from day one?"

## How

- Read every affected file and understand the current design first.
- Ask: "If we wrote this from scratch with this requirement, what would we build?"
- Carry the answer through everything it touches: types, call sites, tests, docs, and examples.
- Design the whole change first, then deliver it in small steps that each work.

This keeps the design easy to change later, instead of piling up special cases that the next change has to work around.

Related: `principle-migrate-callers-then-delete-legacy-apis` for removing the old path once the new design exists.
