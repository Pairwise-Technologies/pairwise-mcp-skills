# AGENTS.md

This repo is public. It tells Pairwise customers how to connect an AI assistant to the hosted Pairwise MCP server, and it holds Agent Skills for using that server. It does not contain or run the server.

## Layout

```
skills/<skill-name>/SKILL.md
```

One folder per skill, one `SKILL.md` per folder. Each `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: <skill-name>        # must match the folder name
description: "<what it does and when to use it>"
---
```

Do not create `.cursor/skills` or `.claude/skills` duplicates.

## Naming

Every skill name starts with `pairwise-`, then a group (`recruiting`, `interviewing`, `delivery`, `domain`) unless the skill is a basic every user needs. See `docs/SKILL_NAMING.md`.

## What may go in this repo

User-facing content only: how to connect, what users can ask, and skills that help an assistant use Pairwise.

Never add:

- How the server works inside: authentication, authorization, tokens, scopes, permission rules, rate limits, hosting or infrastructure.
- Known bugs, weaknesses or security issues. Report those privately (see `CONTRIBUTING.md`).
- Steps for running the server locally, or links to internal docs, tickets or channels.
- Tool names, tool counts or tool parameters. Skills describe each step by what it does ("get the pipeline summary"), so they keep working when tools change.
- Real data: candidate names, emails, company names, IDs, or links that contain real IDs. Use synthetic examples and placeholders.

## Style

- Plain, short sentences. Second person ("you") in the README.
- Product words: **service request** (not job), **evaluation** (not interview), **match score**, **pipeline**, **stage**. Never "fraud" (say "authenticity") and never "guest".
- No em-dashes. Use commas, periods, colons or hyphens.

## Changes

- One skill per PR. Check it against `docs/QUALITY_BAR.md` before you open the PR.
- Add each new skill to the **Skills** section of `README.md`.
- Pairwise maintainers review every PR (`.github/CODEOWNERS`).
- PR descriptions and commit messages are public. Follow "Pull request descriptions" in `CONTRIBUTING.md`.
