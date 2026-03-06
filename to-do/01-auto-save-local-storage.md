# Auto-save & Local Storage

## Priority: High / Quick Win

## Problem
Data is lost on page refresh. Users lose all their work if they accidentally close the tab or navigate away.

## Solution
Save invoice form state to `localStorage` on every change. Restore state on page load.

## Acceptance Criteria
- Invoice form state persists across page refreshes
- User sees their last working state when reopening the app
- A "Clear Form" button allows starting fresh
- Debounce saves to avoid performance issues (e.g., save every 500ms)

## Technical Notes
- Use `localStorage.setItem()` / `getItem()` in `InvoiceForm.js`
- Serialize state with `JSON.stringify()` and restore with `JSON.parse()`
- Consider adding a "last saved" timestamp display
