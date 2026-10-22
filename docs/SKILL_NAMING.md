# SKILL_NAMING

How skills in this repo are named.

## Rule

Every name starts with `pairwise-`, the product the skill works with. After that, order words from least specific to most specific, with the task last as a noun:

```
pairwise-<subject>-<task>
```

This keeps all Pairwise skills together in a sorted skill list, next to the user's other skills.

## Format

These come from the [Agent Skills specification](https://agentskills.io/specification) and break loading if ignored:

- Lowercase letters, digits and single hyphens only.
- At most 64 characters. Aim for 2-4 words.
- The folder name and the `name:` field match exactly.
- No version or phase numbers.

## Word choice

- Use the word people search for, in Pairwise product language: `service-request`, `evaluation`, `pipeline`.
- One word for one thing across all skills.
- Steps in a sequence get distinct task words (`summary`, then `review`).
- Choose names to last. Renaming a skill breaks everything that points at it.

## Test

Sort the existing skill names with the new one. It should land next to its relatives, and a reader should be able to guess what it does from the name alone.
