# Ticket Workflow

## Ticket Structure

Tickets are stored as markdown files in the `to-do/` folder. Each ticket follows this format:

```
# <Feature Title>

## Priority: <High | Medium | Nice to Have> / <Quick Win | Core Feature>

## Problem
<What user pain point does this solve?>

## Solution
<High-level approach>

## Acceptance Criteria
<Bullet list of testable requirements — the definition of "done">

## Technical Notes
<Implementation hints, affected files, dependencies>
```

## Ticket Lifecycle

```
┌──────────┐     ┌─────────────┐     ┌──────────────┐     ┌──────────┐
│ Backlog  │────▶│ In Progress │────▶│ In Review    │────▶│   Done   │
└──────────┘     └─────────────┘     └──────────────┘     └──────────┘
                       │                                        │
                       ▼                                        ▼
                 ┌──────────┐                           Move file to
                 │ Blocked  │                           to-do/done/
                 └──────────┘
```

| Status | What it means |
|--------|--------------|
| **Backlog** | File exists in `to-do/`, no branch created |
| **In Progress** | Feature branch created, work underway |
| **In Review** | PR open, awaiting review |
| **Done** | PR merged, file moved to `to-do/done/` |
| **Blocked** | Waiting on a dependency (noted in file) |

## Picking Up a Ticket

1. **Read the ticket file** — understand the full scope before writing code
2. **Check dependencies** — some tickets depend on others (noted in Technical Notes)
3. **Create a feature branch** — `feature/<ticket-number>-<short-name>`
4. **Implement against acceptance criteria** — every bullet point must be met
5. **Self-test** — manually verify each acceptance criterion
6. **Open PR** — use the PR template from `skills/pr-template.md`

## Priority Guide

Work tickets in this order:

1. **High / Quick Win** — Small effort, high user impact. Do these first.
2. **High** — Important but may require more effort.
3. **Medium / Core Feature** — Foundational features that enable future work.
4. **Nice to Have** — Polish and secondary features.

Within the same priority, prefer tickets with no dependencies over those that are blocked.

## Dependency Map

```
01 Auto-save (no deps)
02 Dynamic PDF filename (no deps)
03 Company Logo Upload → depends on 01 (localStorage for persistence)
04 Email Delivery (no deps, but needs backend)
05 Invoice History → depends on 04 (backend infrastructure)
06 Multiple Templates (no deps)
07 Recurring Invoices → depends on 05, 04
08 Payment Integration → depends on 05
09 Dark Mode (no deps)
10 Multi-language (no deps)
11 Terms & Conditions (no deps)
12 Duplicate Invoice → depends on 05
```

## Scoping Rules

- **Do only what the ticket asks.** Do not add unrequested improvements.
- **If the ticket is ambiguous,** ask for clarification before implementing.
- **If you discover a bug** while working on a ticket, file a new ticket — do not fix it in the same branch unless it directly blocks your work.
- **If the ticket is too large,** propose splitting it into sub-tickets before starting.
