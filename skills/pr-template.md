# Pull Request Template

When creating a PR, use this format for the description:

---

```markdown
## Summary

<!-- 1-3 bullet points explaining WHAT changed and WHY -->

-

## Ticket

<!-- Link to the to-do file this PR addresses -->

Resolves: `to-do/<ticket-file>.md`

## Changes

<!-- List the files modified and what changed in each -->

- `src/components/InvoiceForm.js` — Added localStorage save/restore logic
- `src/components/InvoiceModal.js` — Updated PDF filename to use invoice number

## How to Test

<!-- Step-by-step instructions for verifying the change -->

1. Run `npm start`
2. Fill in invoice fields
3. Refresh the page
4. Verify fields are restored

## Screenshots

<!-- Required for any UI changes. Before/after preferred. -->

| Before | After |
|--------|-------|
| (screenshot) | (screenshot) |

## Checklist

- [ ] Code follows existing patterns (class components, no hooks)
- [ ] No unrelated changes included
- [ ] Tested manually in browser
- [ ] No console errors or warnings introduced
- [ ] PDF export still works correctly
- [ ] Responsive layout not broken (check md/lg breakpoints)
```

---

## PR Title Format

```
<type>: <Short description under 70 chars>
```

Examples:
- `feat: Add auto-save to localStorage`
- `fix: Dynamic PDF filename using invoice number`
- `chore: Update Bootstrap to stable release`

## Rules

- One PR per ticket — do not bundle unrelated changes
- Keep PRs small and focused (under 300 lines changed when possible)
- If a feature is large, break it into stacked PRs with clear dependencies
- Always self-review the diff before requesting review
- Respond to review comments within 24 hours
