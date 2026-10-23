# SKILL_NAMING

How skills in this repo are named.

## Rule

Every name starts with `pairwise-`, the product the skill works with. Next comes the group, then the subject, with the task last as a noun:

```
pairwise-<group>-<subject>-<task>
```

This keeps all Pairwise skills together in a sorted skill list, and keeps each group together inside it.

## Groups

| Group | For | Example |
|---|---|---|
| (none) | Basics every user needs | `pairwise-mcp`, `pairwise-daily-briefing` |
| `recruiting` | Finding and assessing candidates for a service request | `pairwise-recruiting-pipeline-review` |
| `interviewing` | Evaluations: scheduling, feedback and review | `pairwise-interviewing-screen-review` |
| `delivery` | Running service requests across a team or for a client | `pairwise-delivery-briefing` |
| `domain` | Field knowledge that other skills load, no task of its own | `pairwise-domain-engineering-hardware` |

Put a skill in a group when it serves that workflow. Leave the group out only for basics that every Pairwise user needs.

All skills stay in one flat `skills/` folder. Groups live in the name, not in folders, so each skill can still be copied as one folder.

## Format

These come from the [Agent Skills specification](https://agentskills.io/specification) and break loading if ignored:

- Lowercase letters, digits and single hyphens only.
- At most 64 characters.
- The folder name and the `name:` field match exactly.
- No version or phase numbers.

## Word choice

- Use the word people search for, in Pairwise product language: `service-request`, `evaluation`, `pipeline`.
- One word for one thing across all skills.
- Steps in a sequence get distinct task words (`requirements`, then `assessment`).
- Choose names to last. Renaming a skill breaks everything that points at it.

## Test

Sort the existing skill names with the new one. It should land next to its relatives, and a reader should be able to guess what it does from the name alone.
