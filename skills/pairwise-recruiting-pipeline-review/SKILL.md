---
name: pairwise-recruiting-pipeline-review
description: >-
  Review the pipeline of one Pairwise service request or job: how many
  candidates are sourced, contacted, interested and in evaluation, where
  evaluations or interviews stand, and what is waiting on someone. Use when
  the user asks "how is the <role> request (or job) going?", "who is in
  evaluation?", "who is interviewing?", "what is stuck?", or pastes a
  Pairwise pipeline link. Follows the pairwise-mcp skill for words and links.
---

# pairwise-recruiting-pipeline-review

**When to use:** The user wants a status view of one service request's pipeline, or of one stage in it.

**When not to use:** A summary across all service requests (use pairwise-daily-briefing).

Follow the **pairwise-mcp** skill for wording (service request or job, evaluation or interview), links and client visibility. The examples here use services wording.

## Inputs

- The service request: its title, or a Pairwise link. A pipeline link holds the service request ID. A `?candidate=` link also holds an application ID.
- Optional: the stage to focus on, a question ("who is stuck?"), or how many candidates to cover.

## Procedure

1. **Find the service request.** Use the ID from a pasted link, or match the title. If more than one matches, ask which one.
2. **Read the service request** for context: title, status, priority.
3. **Get the status numbers:** sourced, contacted, interested, in evaluation, and any offers, on hold or rejected. Follow "Status of a service request" in the pairwise-mcp skill.
4. **Choose the focus.** If the user did not name one, focus on candidates **in evaluation**, then **interested** candidates. They are the closest to a hire. Look at Sourcing or the rest of Review only when asked, and narrow those first (search text, match score range, location, application date).
5. **List the candidates** in focus, with their application IDs and match scores.
6. **Check the evaluations** for the service request: which are scheduled, which wait for feedback, and which are complete with the evaluator's verdict.
7. **Open full detail** only for the candidates the user asks about, or for those in evaluation, up to 5. Detail shows the step, team notes and each evaluation.
8. **Write the review** (format below).

## Output

```
**<service request link>**: <status>, <priority> priority
<n> sourced · <n> contacted · <n> interested · <n> in evaluation · <offers, on hold, rejected, if not zero>

**<Focus, for example "In evaluation">**
| Candidate | Match score | Latest evaluation | Note |

**Waiting on someone**
- <evaluation link>: <candidate> awaiting feedback from <evaluator> since <date>

**Suggested next steps** (in Pairwise)
- <step>
```

- Link each candidate to their application, and each evaluation to its page.
- "Latest evaluation" is the type, status and verdict, for example "Technical, complete, Yes".
- Keep the note to one line, drawn from team notes or evaluations. Write "No notes" when there are none.
- Mark each note or evaluation that is not shared with the client **(internal)**, as the pairwise-mcp skill says.
- If the user wants the review for a client, list only candidates shared with the client, quote only shared notes and evaluations, and say that you left the rest out.

## Worked synthetic example

User: "How is the Data Engineer request going?"

> **[Data Engineer](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a)**: open, High priority
> 1,204 sourced · 21 contacted · 12 interested · 4 in evaluation · 41 rejected
>
> **In evaluation**
>
> | Candidate | Match score | Latest evaluation | Note |
> |---|---|---|---|
> | [Jordan Lee](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a?candidate=00000000-0000-0000-0000-00000000000b) | 88% | Technical, complete, Yes | Team (internal): "Strong on streaming pipelines." |
> | [Riley Chen](https://app.pairwise.ai/portal/jobs/pipeline/00000000-0000-0000-0000-00000000000a?candidate=00000000-0000-0000-0000-00000000000c) | 81% | Screening, awaiting feedback | No notes |
>
> 2 more candidates are in evaluation. Want them listed too?
>
> **Waiting on someone**
> - [Screening for Riley Chen](https://app.pairwise.ai/portal/jobs/pipeline/interview/00000000-0000-0000-0000-00000000000e) has waited for feedback from the evaluator since Oct 13.
>
> **Suggested next steps** (in Pairwise)
> - Review Jordan Lee's completed evaluations with the team.
> - Remind the evaluator about Riley Chen's screening.
> - Follow up with the 12 interested candidates.

## Failure modes

- **Paging through a huge stage.** Sourcing can hold thousands. Give the count and narrow it before you list anything.
- **Ranking by match score alone.** The match score is one input. Show it next to evaluations and notes, not as the order of merit.
- **Missing verdicts.** An evaluation awaiting feedback has no verdict yet. Say "awaiting feedback", not "no".
- **Missing transcripts.** A transcript can arrive some time after the evaluation. Say it is not available yet.
- **Partial evaluation list.** If the list is cut short, narrow it by status (for example, only awaiting feedback) rather than guessing about the rest.

## Don'ts

- Never repeat a candidate's email, phone number or other contact details unless the user asks.
- Never present a candidate as a hire or a reject. Suggest next steps; people decide.
- Never invent notes, verdicts or dates.
- Never put internal notes or evaluations in an answer meant for a client.
