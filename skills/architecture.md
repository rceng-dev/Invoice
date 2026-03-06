# Architecture Skill

## Design Philosophy

> **Respect the brownfield.** Every architectural decision must consider what already exists. The goal is incremental improvement, not rewrite.

## Decision Framework

When designing a solution, evaluate in this order:

### 1. Can it be done within the existing architecture?

- Can the feature be added with just `this.state` in `InvoiceForm`?
- Can it use existing props drilling?
- Does it fit in the current component tree?

**If yes → do it the simple way.** No new patterns needed.

### 2. Does it require a new component?

- Is the UI complex enough to warrant its own file?
- Will it be reused in multiple places?
- Is it logically separate from existing components?

**If yes → add a new class component** in `src/components/`, wire it into the existing tree.

### 3. Does it require new infrastructure?

- Does it need routing? (e.g., dashboard view)
- Does it need a backend? (e.g., email, database)
- Does it need new libraries?

**If yes → propose the change, explain trade-offs, get approval before implementing.**

## Architectural Constraints

### Hard Constraints (never violate)

1. Client-side React SPA — no SSR, no Next.js
2. Class components — no hooks, no functional components
3. React-Bootstrap for UI — no Material UI, no Tailwind
4. Single state container in `InvoiceForm` — no Redux, no Context API
5. PDF via html2canvas + jsPDF — don't switch to react-pdf or server-side PDF

### Soft Constraints (can be relaxed with justification)

1. No routing — can add `react-router` when dashboard feature is built
2. No backend — can add when email/database features are built
3. No environment variables — can add `.env` when API keys are needed
4. No build config changes — can eject CRA if absolutely necessary

## Common Architecture Decisions

### "Should I add a new library?"

Ask:
1. Does the existing stack already handle this? (Bootstrap utilities, plain JS, etc.)
2. Is the library well-maintained and small? (Check bundle size)
3. Is it compatible with React 17 and CRA 4?

### "Where should new state go?"

**Always in `InvoiceForm.js`** unless:
- It's purely UI state for a self-contained component (e.g., tooltip visibility)
- It's app-level state that exists above InvoiceForm (rare — requires adding state to App.js)

### "Should I refactor the existing code first?"

**No.** Unless the ticket explicitly says to refactor, work within the existing structure. If existing code makes your feature hard to implement, document the friction but work around it.

### "How do I handle the nested setState problem?"

The current `handleCalculateTotal()` uses nested callbacks. When adding calculations:

```js
// Option A: Add to the existing chain (preserves pattern)
this.setState({ newField: value }, () => {
  this.handleCalculateTotal();
});

// Option B: Calculate synchronously and set all at once (better but different pattern)
// Only use if refactoring calculations is part of the ticket
```

## Diagramming New Features

When proposing architecture for a new feature, include:

1. **Component diagram** — where does the new UI live in the tree?
2. **State changes** — what new state fields are needed?
3. **Data flow** — how does data move between components?
4. **File changes** — which files are created/modified?

Example:

```
Feature: Auto-save to localStorage

Component Tree (no changes):
  App → InvoiceForm → [InvoiceItem, InvoiceModal]

New State: none (uses existing state)

Data Flow:
  InvoiceForm.editField()
    → this.setState()
    → componentDidUpdate() [NEW]
    → localStorage.setItem('invoice', JSON.stringify(this.state))

  InvoiceForm.constructor() [MODIFIED]
    → localStorage.getItem('invoice')
    → merge into initial state

Files Modified:
  - src/components/InvoiceForm.js (add componentDidUpdate, modify constructor)

Files Created: none
```
