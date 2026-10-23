---
name: pairwise-mcp
description: >-
  Work with Pairwise hiring data through the Pairwise MCP server: service
  requests, pipelines, candidates, applications and evaluations. Covers
  Pairwise vocabulary, the order to look things up in, how to link every
  service request, candidate and evaluation back to its Pairwise page, and
  what to do when the connection fails. Use for any task that mentions
  Pairwise, a service request, a pipeline or an evaluation, and before the
  other pairwise-* skills.
---

# pairwise-mcp

**When to use:** The user asks about anything in Pairwise: their service requests, a pipeline, a candidate, an evaluation, feedback or notifications.

## Core rules

1. **Know who you are working for.** If it is unclear which account or company is signed in, check the signed-in user first.
2. **Use only what Pairwise returns.** Never guess a candidate, score, status, date or ID. If a lookup returns nothing or is denied, say so plainly.
3. **Send changes to the web app.** If the user asks for something you have no Pairwise action for (create, edit, move, reject, schedule, message), tell them to do it in the Pairwise web app. Never claim a change was made.
4. **People decide.** Summaries, comparisons and match scores help the hiring team. They are not hiring decisions.
5. **Keep candidate data where it is.** Do not copy candidate data into other tools, files or services unless the user asks for that.
6. **Link everything.** See [Links](#links).
7. **Respect what the client can see.** See [Client visibility](#client-visibility).

## Vocabulary

| Pairwise users say | Also called | Notes |
|---|---|---|
| Service request | Job | One role to fill. Data and IDs use the "job" form. Write "service request" to the user. |
| Evaluation | Interview | One assessment of a candidate. Data and IDs use the "interview" form. Write "evaluation" to the user. |
| Application | | One candidate on one service request. |
| Pipeline | | The candidates on one service request, by stage. |
| Stage | | Sourcing, Review, Evaluation, Decision. Decision also has Hold and Rejected. |
| Match score | | Pairwise's fit percentage for a candidate on a service request. Show it as a whole percent (86%). |

## Order of lookups

Start broad, then narrow:

1. **Find the service request.** List the service requests the user can see and match the title. If more than one matches, ask which one.
2. **Pipeline summary.** Get the count per stage before you list candidates.
3. **One stage.** List candidates in the stage the user cares about. Ask for the application ID with each candidate, so you can link to it.
4. **One application.** Open full detail only for the few candidates the user asks about.

Pipelines can be large. Early stages may hold thousands of candidates. Do not page through a whole stage. Narrow it first (search text, match score range, location, application date), and tell the user how many candidates there are and how many you read.

## Links

When you name a service request, candidate or evaluation, make the name a link to its Pairwise page. Build links only from IDs that Pairwise returned in this conversation. If you do not have the ID, give the name without a link. Do not show raw IDs unless the user asks.

| Page | Link |
|---|---|
| Service request pipeline | `https://app.pairwise.ai/portal/jobs/pipeline/{service_request_id}` |
| A candidate's application on a service request | `https://app.pairwise.ai/portal/jobs/pipeline/{service_request_id}?candidate={application_id}` |
| An evaluation | `https://app.pairwise.ai/portal/jobs/pipeline/interview/{evaluation_id}` |
| A candidate's profile | `https://app.pairwise.ai/portal/hiring/{candidate_id}` |

Which candidate link to use:

- Talking about a candidate **on one service request** (pipeline, stage, evaluation): link the application.
- Talking about a candidate **in general**: link the profile.

The application link needs the **application ID**, even though the URL says `candidate=`. A candidate ID in that slot opens the pipeline without the candidate.

## Client visibility

Some companies hire for a client and share candidates with that client. Pairwise marks three things as shared with the client or not: each application, each feedback note, and each evaluation's scorecard.

- When you quote a note or an evaluation that is not shared with the client, mark it **(internal)**.
- If the user says the answer is for a client, include only shared applications, shared notes and shared evaluations. Tell the user that you left the rest out.
- Notifications do not say whether feedback is shared. Treat team and leadership feedback in notifications as internal.

## Worked synthetic example

User: "How is the Data Engineer request going?"

1. Find the service request titled Data Engineer. One match.
2. Get its pipeline summary: Sourcing 1,204, Review 63, Evaluation 4, Decision 1.
3. List the Decision stage with application IDs: one candidate, Jordan Lee.

Answer:

> [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) has 1,204 candidates in Sourcing, 63 in Review, 4 in Evaluation and 1 in Decision. [Jordan Lee](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a?candidate=00000000-0000-0000-0000-00000000000b) is waiting in Decision.

## Connection problems

- **No Pairwise data, or asked to sign in again:** the user needs to sign in again. Sessions expire.
- **"Your account is not eligible for MCP.":** Pairwise MCP is for Pairwise customers with a registered company account. Suggest the user contact support@pairwise.ai.
- **Permission denied on one item:** the user cannot see it in the web app either. Suggest they ask their company's Pairwise admin.
- **Any other error:** retry once. If it fails again, suggest the user email support@pairwise.ai with what they asked and the error text.

## Don'ts

- Never invent IDs, links, scores or candidate details.
- Never use a candidate ID in an application link.
- Never present a summary or match score as a decision to hire or reject.
- Never draw conclusions about age, gender, ethnicity, health, family status or other protected characteristics.
