---
name: principle-naming
description: "Apply when naming or renaming anything in code, and when self-reviewing a diff. Name each thing for what it means to the reader at its point of use."
---

# Naming

A name should tell a reader at the point of use what the thing is, without opening its definition.

- **Meaning over mechanism.** Name what it is or does for its user, not how it is built or called.
- **The reader's vocabulary.** Use the terms of the domain and the caller, not the owner's internal state.
- **Context carries part of the name.** Leave out what the surrounding scope already says; add it back where the name travels beyond that scope.
- **One concept, one name.** Reuse an existing name for the same concept. Precedent decides consistency, not quality: don't copy a nearby name that breaks these rules; name the new code well and flag the old name for a rename.

Check: read each new or changed name where it is used. If it needs its definition to be understood, rename it and update every use in the same change.
