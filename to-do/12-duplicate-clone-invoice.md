# Duplicate / Clone Invoice

## Priority: Nice to Have

## Problem
Users with repeat clients must re-enter the same information for every invoice.

## Solution
Allow one-click duplication of an existing invoice with auto-incremented number.

## Acceptance Criteria
- "Duplicate" button on each invoice in the history dashboard
- Cloned invoice has a new auto-incremented invoice number
- All fields copied except dates (set to today / default due date)
- Status set to "Draft"
- User can edit before saving

## Technical Notes
- Depends on Invoice History feature (#05)
- Deep clone the invoice object, update number and dates
- Navigate to form view with pre-filled data
