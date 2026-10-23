---
name: pairwise-mcp
description: >-
  Work with Pairwise hiring data through the Pairwise MCP server: service
  requests (jobs), pipelines, candidates, applications and evaluations
  (interviews). Covers Pairwise vocabulary and when to use services or
  internal hiring wording, the order to look things up in, how to link every
  service request, candidate and evaluation back to its Pairwise page, and
  what to do when the connection fails. Use for any task that mentions
  Pairwise, a service request or job, a pipeline, or an evaluation or
  interview, and before the other pairwise-* skills.
---

# pairwise-mcp

**When to use:** The user asks about anything in Pairwise: their service requests or jobs, a pipeline, a candidate, an evaluation or interview, feedback or notifications.

## Core rules

1. **Know who you are working for.** If it is unclear which account or company is signed in, check the signed-in user first.
2. **Use only what Pairwise returns.** Never guess a candidate, score, status, date or ID. If a lookup returns nothing or is denied, say so plainly.
3. **Send changes to the web app.** If the user asks for something you have no Pairwise action for (create, edit, move, reject, schedule, message), tell them to do it in the Pairwise web app. Never claim a change was made.
4. **People decide.** Summaries, comparisons and match scores help the hiring team. They are not hiring decisions.
5. **Keep candidate data where it is.** Do not copy candidate data into other tools, files or services unless the user asks for that.
6. **Link everything.** See [Links](#links).
7. **Respect what the client can see.** See [Client visibility](#client-visibility).

## Vocabulary

Pairwise serves two kinds of hiring teams, and each has its own words for the same things. Both sets are correct.

| Concept | Services wording (default) | Internal hiring wording | In Pairwise data |
|---|---|---|---|
| A role to fill | Service request ("request" for short) | Job | job |
| One assessment of a candidate | Evaluation | Interview, or evaluation | interview |
| The person who assesses | Evaluator | Interviewer | interviewer |
| One candidate on one role | Application | Application | application |
| The candidates on one role, by stage | Pipeline | Pipeline | pipeline |
| Pairwise's fit percentage for a candidate on a role | Match score | Match score | score |

Show match scores as a whole percent (86%).

### Which words to use

- **Services wording is the default.** Staffing, recruiting and professional services firms hire for their clients, and they say "service request" and "evaluation".
- **Switch to internal wording when there is evidence** that the company hires for itself:
  - The user says "job", "interview", "role", "req" or "headcount".
  - The user talks about their own team ("our engineering team", "we are hiring").
  - No clients appear anywhere: no client feedback, nothing shared with a client.
- **Stay with services wording** when the user mentions a client, client feedback, or sharing candidates with a client.
- **Mirror the user.** If the user uses one word, answer with the same word. Never correct the user's word.
- **Stay consistent.** Once you choose, use the same words for the rest of the conversation, unless the user switches.
- **Pairwise data does not tell you which kind of company it is.** Its fields always use the job and interview names. Choose by the evidence above.

The rest of this skill, and the other pairwise-* skills, use services wording. Swap in internal wording when you have chosen it.

## Pipeline stages

The pipeline has four stages. Each candidate is also at one step inside their stage:

| Stage | Steps | What it means |
|---|---|---|
| Sourcing | Applied, AI recommended, Added | Candidates found for the role, not yet contacted. |
| Review | Shortlist, Contacted, Interested | Outreach: shortlisted, contacted, then confirmed interest. |
| Evaluation | Evaluating, Evaluations completed | Candidates going through evaluations. |
| Decision | Pending offer, Offer, Not interested, Hold | Where a candidate ends up. Rejected candidates are counted separately. |

Decision is an end point, not a queue. Do not treat it as "waiting for a decision", and do not lead with it.

## Order of lookups

Start broad, then narrow:

1. **Find the service request.** List the service requests the user can see and match the title. If more than one matches, ask which one.
2. **Pipeline summary.** Get the count per stage before you list candidates.
3. **One stage.** List candidates in the stage the user cares about. Ask for the application ID with each candidate, so you can link to it.
4. **One application.** Open full detail only for the few candidates the user asks about.

Pipelines can be large. Early stages may hold thousands of candidates. Do not page through a whole stage. Narrow it first (search text, match score range, location, application date), and tell the user how many candidates there are and how many you read.

## Status of a service request or job

When the user asks how a service request is going, give the numbers a recruiter tracks:

1. **Sourced:** the Sourcing count.
2. **Contacted** and **Interested:** list Review with each candidate's step, and count the steps. Mention Shortlist only if the user asks. If Review holds more than about 500 candidates, give the Review total and offer to count the steps.
3. **In evaluation:** the Evaluation count.
4. **Offers, on hold, rejected:** count offers from the Decision list, and get the on-hold and rejected counts separately. The pipeline summary's Decision count leaves out on-hold and rejected candidates.

Leave out any number that is zero. Do not list stage names for their own sake.

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
2. Get its pipeline summary: Sourcing 1,204, Review 63, Evaluation 4.
3. List Review with each candidate's step: 30 Shortlist, 21 Contacted, 12 Interested.
4. Get the on-hold and rejected counts: 0 on hold, 41 rejected. The Decision list has no offers.

Answer:

> [Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a) so far:
>
> - 1,204 candidates sourced
> - 21 contacted
> - 12 interested
> - 4 in evaluation, including [Jordan Lee](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a?candidate=00000000-0000-0000-0000-00000000000b)
> - 41 rejected
>
> Want the list of interested candidates?

On hold and offers are left out because they are zero.

### Internal hiring wording

User: "How many people have we interviewed for the Product Designer job?"

The user says "job" and "we", so answer in internal hiring wording:

> On the [Product Designer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000f) job, 6 candidates have finished their interviews and 3 more are interviewing now.

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
