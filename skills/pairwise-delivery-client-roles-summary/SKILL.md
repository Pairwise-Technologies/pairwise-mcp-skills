---
name: pairwise-delivery-client-roles-summary
description: >-
  Summarize the open service requests a recruiting team is working on for its
  clients: for each client, every role's priority, location, recent activity
  and candidates in evaluation, with quiet roles flagged and an optional nudge
  message for the recruiting team. Use when a delivery, account or recruiting
  manager asks "how are we doing on <client>'s roles?", "which roles need
  attention?", "which roles have gone quiet?", or wants a client roles report.
  Follows the pairwise-mcp skill.
---

# pairwise-delivery-client-roles-summary

**When to use:** A manager at a staffing or professional services company wants one view of the roles their recruiters work on for a client, or for all clients, and which roles have gone quiet.

**When not to use:** A deep look at one service request (use pairwise-recruiting-pipeline-review). A personal "what's new" (use pairwise-daily-briefing).

Follow the **pairwise-mcp** skill for wording, links and client visibility.

## Inputs

- **Client:** optional. Default: all clients.
- **Window:** optional. Default: 14 days. A role is quiet when nothing happened on it in the window.
- **Groups:** optional. Default: one table per client. Split further only when the user asks, for example by country, region or recruiting team.
- **Nudge message:** optional. Draft it when the user asks, or offer it when there are quiet roles.

## Activity: what to measure

**Preferred:** profiles shared with the client. For each service request, the date the last profile was shared and how many are shared now. Use this when Pairwise gives it to you directly for a service request.

**Fallback:** if Pairwise does not give it directly, do not open every candidate to find share dates. That takes hundreds of lookups. Measure recent recruiting activity instead:

- Count the candidates **added in the window** who are now in **Review** or **Evaluation** (shortlisted, contacted, interested or being evaluated). Use the added-date filter on those two stage lists and read the totals.
- Label the column "New in review or evaluation (last 14 days)". Say once in the report that it measures recruiting activity, not what the client has seen.

Do not count Sourcing. Pairwise adds recommended candidates to Sourcing on its own, so new Sourcing candidates do not mean that the team worked the role. Never mix the two measures in one column.

## Procedure

1. **Check the signed-in user** and their company.
2. **List open service requests.** Leave out the ones on hold, in draft, filled or closed. Count those on hold to mention them.
3. **Read each service request's details** for its client, priority and locations. This is one lookup per service request.
   - If the user named a client, keep only that client's service requests. Match the name without case. If nothing matches, show the client names you found and ask.
   - If no service request has a client, the company hires for itself. Skip the client grouping, and use internal hiring wording (job, interview).
4. **Measure activity** for each kept service request (see above), and get the count **in evaluation** from its pipeline summary.
5. **Flag quiet roles:** no activity in the window. With the preferred measure: no profile shared in the window, or none shared at all.
6. **Sort** each table by priority (High, Mid, Low), then by title.
7. **Write the report** (format below).
8. **Offer the nudge message** if any role is quiet.

## Output

```
## <Client>: open service requests, as of <date>

<n> open · <n> need attention · <n> on hold (not shown)

| Service request | Priority | Location | New in review or evaluation (last 14 days) | In evaluation |
|---|---|---|---|---|
| <link> | High | <location> | **0** | <n> |

**Needs attention**
- <link> (<priority>, <location>): nothing new in review or evaluation in the last 14 days.
```

- One section per client. Order clients by their number of quiet roles, most first.
- Link each service request to its pipeline. Show several locations as "Seattle, WA +2".
- Mark quiet roles in bold in the activity column.
- With the preferred measure, use the columns "Last profile shared" and "Shared now", and write "None shared yet" when there are none. Never invent a date.

**Nudge message**, as plain text in a code block so the user can copy it. The user picks the roles and edits the wording:

```
Hi team, please give more attention to the roles below. Nothing new has moved forward on them in the last two weeks.

• <Title> (<priority> priority, <location>)
  <pipeline link>

Please share new profiles as soon as you have them. Thank you!
```

## Worked synthetic example

User: "How are we doing on Northwind's roles?"

> ## Northwind: open service requests, as of Oct 23
>
> 3 open · 1 needs attention · 1 on hold (not shown)
>
> Activity counts candidates added in the last 14 days who are now in review or evaluation. It shows recruiting activity, not what Northwind has seen.
>
> | Service request | Priority | Location | New in review or evaluation (last 14 days) | In evaluation |
> |---|---|---|---|---|
> | [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) | High | Seattle, WA | **0** | 1 |
> | [Account Executive](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000c) | High | Austin, TX +1 | 14 | 3 |
> | [Product Designer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000f) | Mid | Remote | 6 | 0 |
>
> **Needs attention**
> - [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) (High, Seattle, WA): nothing new in review or evaluation in the last 14 days.
>
> Want a nudge message for the recruiting team?

## Failure modes

- **Opening every candidate to find share dates.** Too slow. Use the fallback measure.
- **Counting Sourcing as activity.** It fills on its own. Count Review and Evaluation only.
- **Added date is not move date.** A candidate added a month ago and contacted today does not count in the window. Say so if the user questions a quiet role.
- **Client names differ** ("Northwind", "Northwind Inc."). Group names that clearly match, and ask when unsure.
- **Partial list.** If the list of service requests may be cut short, say how many you covered.
- **Old results.** Look everything up again on each run. Never reuse roles, dates or counts from an earlier answer.

## Don'ts

- Never send the nudge message. Draft it for the user to send.
- Never list recruiters' or hiring team members' names or emails unless the user asks.
- Never put candidate details in this report. It is about roles, so counts are enough.
- Never show internal notes in a report meant for the client.
- Never invent dates or counts. If a number is not available, say so.
