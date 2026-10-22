# QUALITY_BAR

A skill in this repo helps an AI assistant work with Pairwise for a Pairwise user. Someone who has never seen the skill should be able to follow it from the file alone: when to use it, what to gather, what steps to take, and what a good answer looks like.

Skills **assist** hiring teams. They do not hire, reject or decide for anyone. Any comparison or summary is a draft for a person to review.

## Completeness checklist

| Section | Required content |
|---|---|
| Frontmatter | `name` (matches the folder, follows `docs/SKILL_NAMING.md`) and `description` |
| Title + when to use | 1-2 lines: the skill name and the situation that triggers it |
| Inputs | What the user gives, or what the assistant must find first |
| Procedure | Numbered, concrete steps, each described by what it does, not by tool name |
| Output | What a good answer looks like, with links to the Pairwise pages it mentions |
| Worked synthetic example | One short example with fake names and placeholder IDs |
| Failure modes | What usually goes wrong, and what to do instead |
| Don'ts | Hard bans |

Target length: roughly 40-100 lines.

## Content rules

- User-facing only. Follow "What may go in this repo" in `AGENTS.md`.
- No tool names, tool counts or parameters.
- Synthetic examples only. No real people, companies, IDs or links that contain real IDs.
- Use only what Pairwise returns. Never guess a candidate, score, status or ID.
- To change something, the user goes to the Pairwise web app. A skill never claims a change was made.
- No em-dashes.

## Landing bar

Do not merge a skill unless:

1. It passes the checklist above.
2. Someone has run it against the live Pairwise MCP server with a real account and checked the answer.
3. A Pairwise maintainer has reviewed it. A self-check by an agent does not count as review.
