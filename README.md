# skillKit

Portable agent skills: playbooks, principles and workflows that hold for any person, company, project or agent harness.

## What belongs here

A skill belongs here when it would read the same in a different company. Keep out:

- Facts about a person or workspace: names, handles, file paths, secrets locations, tool accounts. These go in `AGENTS.md`.
- Company systems: internal services, runbooks, schemas, brand rules, team processes. These go in custom skills that live only in that workspace.
- Point-in-time data: dates, ticket numbers, metrics from one investigation.

A generic skill that needs a local fact names what it needs ("the secrets file named in `AGENTS.md`"), not the value.

## AGENTS.md

Each workspace keeps one `AGENTS.md` that holds its own preferences and facts. It is not part of this repo. Point every harness's instruction file at it, so there is one copy to edit:

    ln -s ~/path/to/workspace/AGENTS.md ~/.claude/CLAUDE.md

## Linking skills

Harnesses read one flat skills folder. Keep that folder outside this repo, link it into each harness, and link each skill here into it individually. Custom skills live in the same folder as real directories.

    mkdir -p ~/skills
    ln -sfn ~/skills ~/.claude/skills
    ln -sfn ~/skills ~/.agents/skills
    for d in ~/path/to/skillKit/*/; do ln -sfn "${d%/}" ~/skills/; done

Relink after adding or renaming a skill, and delete the link of a removed one. Edits to existing skills need no relink, because the links point at this checkout.
