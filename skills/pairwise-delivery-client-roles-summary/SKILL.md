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

**Profiles shared with the client.** This is what the client sees, so it is the measure to use. For each service request, list its candidates at every stage, outcomes included, since by default only candidates still in progress are listed:

- **Last profile shared:** sort that list by most recently shared and read the first row's share date. If that row has no share date, none have been shared.
- **Shared in the window:** list the candidates shared with the client since the start of the window, in the user's time zone when you know it, and read the total.

Each is one short lookup per service request. Never open every candidate to find share dates.

**Service requests with no client** have nobody to share with. For those, measure recruiting activity instead: count the candidates **added in the window** who are now shortlisted, contacted, interested or evaluating. List those four stages together with the added-to-pipeline date set to the window, and read the total. Do not count Sourcing: Pairwise adds recommended candidates there on its own, so new Sourcing candidates do not mean the team worked the role. Label this column "New in review or evaluation (last 14 days)", and never mix it with the shared measure in one column.

## Procedure

1. **Check the signed-in user** and their company.
2. **Search for open service requests,** with candidate counts per stage on each row. Leave out the ones on hold, in draft, filled or closed. Search on hold status too, and use its total to mention how many are on hold. Each row gives the client and priority.
   - If the user named a client, keep only that client's service requests. Match the name without case. If nothing matches, show the client names you found and ask.
   - If no service request has a client, the company hires for itself. Skip the client grouping, and use internal hiring wording (job, interview).
3. **Read each kept service request's full record** for its locations. This is one lookup per service request.
4. **Measure activity** for each kept service request (see above). The count **in evaluation** is on its search row.
5. **Flag quiet roles:** no profile shared in the window, or none shared at all. For a service request with no client: nothing new in review or evaluation in the window.
6. **Sort** each table by priority (High, Mid, Low), then by title.
7. **Write the report** (format below).
8. **Offer the nudge message** if any role is quiet.

## Output

```
## <Client>: open service requests, as of <date>

<n> open · <n> need attention · <n> on hold (not shown)

| Service request | Priority | Location | Last profile shared | Shared (last 14 days) | In evaluation |
|---|---|---|---|---|---|
| <link> | High | <location> | <date> | **0** | <n> |

**Needs attention**
- <link> (<priority>, <location>): no profile shared in the last 14 days.
```

- One section per client. Order clients by their number of quiet roles, most first.
- Link each service request to its pipeline. Show several locations as "Seattle, WA +2".
- Mark quiet roles in bold in the activity column.
- Write "None shared yet" when no profile has been shared. Never invent a date.
- For service requests with no client, replace the two shared columns with "New in review or evaluation (last 14 days)", and say once that it measures recruiting activity, not what a client has seen.

**Nudge message**, as plain text in a code block so the user can copy it. The user picks the roles and edits the wording:

```
Hi team, please give more attention to the roles below. No new profiles have been shared on them in the last two weeks.

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
> | Service request | Priority | Location | Last profile shared | Shared (last 14 days) | In evaluation |
> |---|---|---|---|---|---|
> | [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) | High | Seattle, WA | Sep 30 | **0** | 1 |
> | [Account Executive](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000c) | High | Austin, TX +1 | Oct 22 | 5 | 3 |
> | [Product Designer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000f) | Mid | Remote | Oct 17 | 2 | 0 |
>
> **Needs attention**
> - [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) (High, Seattle, WA): no profile shared since Sep 30.
>
> Want a nudge message for the recruiting team?

## Failure modes

- **Opening every candidate to find share dates.** Too slow. The candidate list gives share dates; one sorted lookup per service request is enough.
- **Listing only candidates in progress.** A shared candidate may since have been hired or rejected. Include every stage and outcome when you look for share dates.
- **Counting Sourcing as activity** (no-client roles). It fills on its own. Count shortlisted, contacted, interested and evaluating only.
- **Added date is not move date** (no-client roles). A candidate added a month ago and contacted today does not count in the window. Say so if the user questions a quiet role.
- **Client names differ** ("Northwind", "Northwind Inc."). Group names that clearly match, and ask when unsure.
- **Partial list.** If the list of service requests may be cut short, say how many you covered.
- **Old results.** Look everything up again on each run. Never reuse roles, dates or counts from an earlier answer.

## Don'ts

- Never send the nudge message. Draft it for the user to send.
- Never list recruiters' or hiring team members' names or emails unless the user asks.
- Never put candidate details in this report. It is about roles, so counts are enough.
- Never show internal notes in a report meant for the client.
- Never invent dates or counts. If a number is not available, say so.
