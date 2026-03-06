# Meeting Notes Skill

## Purpose

Extract structured, actionable information from meeting transcripts, chat logs, or verbal summaries. Produce artifacts that feed directly into the development workflow.

## Input

The agent receives raw meeting content — this can be:
- A transcript (formatted or unformatted)
- Chat/Slack messages
- A verbal summary from the user
- Voice-to-text output (may have errors)

## Output Format

```markdown
# Meeting Notes — <Date> — <Meeting Title/Topic>

## Attendees
- <Name> (<Role>)

## Decisions Made
<!-- Things that were agreed upon — these are final -->
1. <Decision>
2. <Decision>

## Action Items
<!-- Tasks assigned to specific people with deadlines -->
| # | Action | Owner | Deadline | Ticket |
|---|--------|-------|----------|--------|
| 1 | <task> | <who> | <when>   | <link to to-do file or "NEW"> |

## Backlog Updates
<!-- Changes to existing tickets based on meeting discussion -->
- **<ticket>**: <what changed — priority, scope, acceptance criteria, etc.>

## Deferred / Parked
<!-- Topics raised but explicitly pushed to a later date -->
- <Topic> — deferred to <when/why>

## Open Questions
<!-- Unresolved items that need follow-up -->
- <Question> — needs input from <who>

## Raw Notes
<!-- Optional: key quotes or context that didn't fit above -->
```

## Processing Rules

1. **Decisions vs. Opinions** — Only list something as a "Decision" if the group clearly agreed. Suggestions, preferences, and debates go in "Raw Notes."

2. **Action Items must be specific** — "Look into caching" is not actionable. "Research Redis vs localStorage for auto-save and propose approach by Friday" is.

3. **Map to existing tickets** — If a discussion topic maps to an existing `to-do/` file, reference it. If it's a new task, mark it as "NEW" and offer to create the ticket.

4. **Flag conflicts** — If a decision contradicts an existing ticket's scope or acceptance criteria, call it out explicitly.

5. **Capture deferrals** — When the team says "let's do that in Q3" or "not now", capture it in Deferred with the reasoning.

6. **Handle ambiguity** — If the transcript is unclear, flag it as an Open Question rather than guessing.

## After Processing

Offer to:
1. Create new `to-do/` tickets for action items marked "NEW"
2. Update existing `to-do/` files with changed requirements
3. Update priority ordering based on decisions
4. Create a summary for async team members who missed the meeting

## Example

**Input:**
> "So John said he wants the invoice to support recurring billing, but Sarah said that's too complex for now. They agreed to just add a 'Terms & Conditions' field first since it's quick. Mike wants the PDF filename fixed — it always says invoice-001."

**Output:**

```markdown
## Decisions Made
1. Add Terms & Conditions field before recurring billing
2. Fix PDF filename to use actual invoice number

## Action Items
| # | Action | Owner | Deadline | Ticket |
|---|--------|-------|----------|--------|
| 1 | Implement Terms & Conditions field | — | — | to-do/11-terms-and-conditions.md |
| 2 | Fix dynamic PDF filename | — | — | to-do/02-dynamic-pdf-filename.md |

## Backlog Updates
- **to-do/11-terms-and-conditions.md**: Priority elevated — team wants this before recurring invoices
- **to-do/07-recurring-invoices.md**: Deferred — team considers it too complex for current sprint

## Deferred / Parked
- Recurring billing — deferred, deemed too complex for now (Sarah's recommendation, group agreed)
```
