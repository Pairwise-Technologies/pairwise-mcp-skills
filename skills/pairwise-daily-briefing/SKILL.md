---
name: pairwise-daily-briefing
description: >-
  Give a Pairwise user a short briefing on what needs their attention: open
  service requests with candidates waiting, and recent feedback, offers and
  team changes from their notifications. Use when the user asks "what's new
  in Pairwise?", "what needs my attention today?", or wants a morning or
  weekly hiring summary. Follows the pairwise-mcp skill for words and links.
---

# pairwise-daily-briefing

**When to use:** The user wants a quick view of their Pairwise work, for today or for a period they name.

**When not to use:** A deep look at one service request (use pairwise-pipeline-review).

Follow the **pairwise-mcp** skill for vocabulary and links.

## Inputs

- Optional: a time window ("today", "since Monday"). Default: the last 24 hours, or since the last working day.
- Optional: a focus, such as one service request or only feedback.

## Procedure

1. **Dashboard.** Get the user's dashboard: their open service requests with candidate counts per stage, pinned ones first, plus how many are in draft or on hold.
2. **Notifications.** Get the newest notifications. Load more pages only until the items are older than the time window, and stop after about 100 items.
3. **Drop the user's own actions.** Items the user did themselves are not news to them.
4. **Group the notifications:**
   - Feedback: from the team, the client, or leadership, on a candidate.
   - Offers made.
   - Team changes: the user was added to or removed from a service request.
   - Priority changes on a service request.
5. **Pick what needs attention.** Name only what the data shows, for example:
   - Candidates waiting in Decision.
   - New feedback on a candidate.
   - Offers made.
   - A service request whose priority went up.
6. **Write the briefing** (format below). Keep it short. The user can ask for more.

## Output

```
**Needs attention**
- <item, with links>

**Feedback and offers** (<time window>)
- <who> on <candidate link> for <service request link>: <one-line gist>

**Open service requests**
| Service request | Priority | Review | Evaluation | Decision |

<one line: how many more are open, and draft and on-hold counts>
```

- In the table, show pinned service requests and those with candidates in Evaluation or Decision. Show at most 10 rows, and count the rest in the line below.

- Link each service request to its pipeline, and each candidate to their application. Notifications about a candidate carry both IDs.
- Quote feedback in one short line. Do not turn a rating into a number the user did not see.
- Client feedback may show a reviewer with no real name. Call them "the client".

## Worked synthetic example

User: "What needs my attention in Pairwise today?"

> **Needs attention**
> - [Jordan Lee](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a?candidate=00000000-0000-0000-0000-00000000000b) is waiting in Decision on [Senior Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a).
>
> **Feedback and offers** (last 24 hours)
> - The client on [Sam Ortiz](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000c?candidate=00000000-0000-0000-0000-00000000000d) for [Field Applications Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000c): "Strong on customer demos, wants more depth on firmware."
>
> **Open service requests**
>
> | Service request | Priority | Review | Evaluation | Decision |
> |---|---|---|---|---|
> | [Senior Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) | High | 63 | 4 | 1 |
> | [Field Applications Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000c) | Mid | 18 | 2 | 0 |
>
> 3 more service requests are open. 2 are in draft and 1 is on hold.

## Failure modes

- **"New" is not "unread here".** Pairwise marks notifications new until the user opens them in the web app. Reading them through the assistant does not change that, so the same items can show as new on every briefing. Use the time window, not the "new" flag.
- **On-hold service requests** appear only as a count on the dashboard. Look them up by name if the user asks.
- **Empty dashboard:** the user may have no open service requests, or no access to any. Say so and suggest they check the web app.
- **Too much to show:** summarize counts per group and list only the top items.

## Don'ts

- Never invent urgency the data does not show.
- Never list the user's own actions as news.
- Never mark anything as handled or read. The assistant cannot change Pairwise.
