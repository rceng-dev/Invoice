# Product Management Skill

## Purpose

Analyze the product from a user and business perspective. Identify gaps, prioritize features, write specs, and maintain the backlog.

## Capabilities

### 1. Requirements Analysis

When given a user request, customer feedback, or business goal:

1. **Understand the user pain point** — What problem are they actually trying to solve?
2. **Map to existing backlog** — Does a ticket already address this? Partially?
3. **Assess scope** — Is this a quick win, a feature, or an epic?
4. **Identify dependencies** — What must exist before this can be built?
5. **Write acceptance criteria** — Specific, testable, unambiguous

### 2. Backlog Management

The backlog lives in `to-do/`. The agent can:

- **Create new tickets** — When a requirement doesn't map to an existing ticket
- **Update existing tickets** — When scope, priority, or criteria change
- **Re-prioritize** — Based on user feedback, business goals, or technical dependencies
- **Identify duplicates** — Merge overlapping tickets
- **Split epics** — Break large tickets into deliverable increments

### 3. Feature Specification

When writing a new ticket in `to-do/`, follow this template:

```markdown
# <Feature Title>

## Priority: <High | Medium | Nice to Have> / <Quick Win | Core Feature>

## Problem
<1-2 sentences describing the user pain point>

## Solution
<1-2 sentences describing the approach>

## Acceptance Criteria
- <Testable criterion 1>
- <Testable criterion 2>
- <Testable criterion 3>

## Technical Notes
- <Implementation hints>
- <Affected files>
- <Dependencies on other tickets>
```

### 4. User Feedback Processing

When the user shares customer feedback:

1. **Extract discrete requests** — Separate compound feedback into individual items
2. **Classify each request:**
   - Bug — Something is broken
   - Feature — Something new is needed
   - Improvement — Something existing needs to be better
   - Question — Needs clarification, not a ticket
3. **Map to backlog** — Link to existing tickets or create new ones
4. **Prioritize** — Use the impact/effort matrix below

### 5. Prioritization Framework

```
                    High Impact
                        │
        ┌───────────────┼───────────────┐
        │   QUICK WINS  │   BIG BETS    │
        │   Do first    │   Plan next   │
        │               │               │
Low ────┼───────────────┼───────────────┼──── High
Effort  │               │               │   Effort
        │   FILL-INS    │   MONEY PITS  │
        │   Do if idle  │   Avoid/defer │
        │               │               │
        └───────────────┼───────────────┘
                        │
                    Low Impact
```

| Quadrant | Action | Current tickets |
|----------|--------|-----------------|
| Quick Wins | Do immediately | 01, 02, 03, 09, 11 |
| Big Bets | Plan carefully, validate ROI | 05, 06, 08 |
| Fill-ins | Nice to have, low priority | 10, 12 |
| Money Pits | Defer or descope | 07 (without 05 built first) |

## Rules

1. **User value first** — Every feature must tie back to a user benefit
2. **One problem per ticket** — If a ticket solves two problems, split it
3. **Acceptance criteria are non-negotiable** — If it's not in the criteria, it's not in scope
4. **Say no to scope creep** — If implementation reveals new requirements, create a new ticket
5. **Dependencies are blockers** — Don't start a ticket if its dependency isn't done
