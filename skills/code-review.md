# Code Review Skill

## Purpose

Review code changes (PRs, diffs, or staged files) for quality, consistency, correctness, and adherence to project conventions.

## Review Checklist

### 1. Pattern Compliance

- [ ] Uses class components (no hooks, no functional components)
- [ ] State managed via `this.state` / `this.setState()` only
- [ ] UI built with React-Bootstrap components
- [ ] Import order: React → Bootstrap → Local → Utilities
- [ ] Naming matches existing conventions (camelCase state, PascalCase components)
- [ ] No TypeScript, no PropTypes added

### 2. Brownfield Discipline

- [ ] No unrelated refactoring included
- [ ] No "while I'm here" improvements
- [ ] Existing patterns followed even if imperfect (e.g., `var` usage in older files)
- [ ] Technical debt not fixed unless ticket explicitly requests it
- [ ] The `taxAmmount` / `discountAmmount` typos preserved (unless ticket says fix)

### 3. Correctness

- [ ] Acceptance criteria from the ticket are fully met
- [ ] Edge cases handled (empty items, zero values, missing fields)
- [ ] No `console.log` left in code
- [ ] No hardcoded values that should be dynamic
- [ ] Calculations produce correct results (check `handleCalculateTotal` integration)

### 4. UI/UX

- [ ] Responsive layout works at `md` and `lg` breakpoints
- [ ] Form validation present on required fields
- [ ] Bootstrap utility classes used (not custom CSS) where possible
- [ ] Invoice preview in modal renders correctly
- [ ] PDF export captures all visible content

### 5. Safety

- [ ] No direct state mutation in new code (even though existing code does it)
- [ ] No security issues (XSS via dangerouslySetInnerHTML, eval, etc.)
- [ ] No sensitive data logged or exposed
- [ ] File operations (localStorage, downloads) have error handling

### 6. Scope

- [ ] Changes are limited to what the ticket requires
- [ ] No new dependencies added without justification
- [ ] No files modified that aren't related to the ticket
- [ ] PR is reasonably sized (under 300 lines preferred)

## Review Output Format

```markdown
## Review: <PR Title>

### Verdict: <Approve | Request Changes | Comment>

### Summary
<1-2 sentences on the overall quality of the change>

### Issues
<!-- Only include sections that have findings -->

#### Must Fix (Blocks merge)
1. **<File:Line>** — <Description of issue>
   ```js
   // Suggested fix
   ```

#### Should Fix (Non-blocking but important)
1. **<File:Line>** — <Description>

#### Nit (Style/preference, optional)
1. **<File:Line>** — <Description>

### What's Good
<!-- Call out things done well — positive reinforcement -->
- <Something done correctly>
```

## Review Principles

1. **Be specific** — "This looks wrong" is not helpful. "This will crash when items is empty because `splice(-1, 1)` removes the last element" is.
2. **Suggest fixes** — Don't just point out problems, show the solution.
3. **Distinguish severity** — Not everything is a blocker. Use Must Fix / Should Fix / Nit.
4. **Respect the author** — Review the code, not the person. Use "this code" not "you."
5. **Check the ticket** — Review against acceptance criteria, not your personal preferences.
