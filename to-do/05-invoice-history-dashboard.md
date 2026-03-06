# Invoice History & Dashboard

## Priority: Medium / Core Feature

## Problem
No way to view, retrieve, or manage past invoices. The app is a one-shot PDF generator.

## Solution
Persist invoices to a database and provide a dashboard to list, search, and manage them.

## Acceptance Criteria
- Save invoices to a database (Firebase Firestore)
- Dashboard view listing all invoices with key info (number, client, amount, date, status)
- Status tracking: Draft, Sent, Paid, Overdue
- Search and filter by client name, date range, status
- Click to view/edit any past invoice
- Delete invoices with confirmation

## Technical Notes
- Firebase Firestore is already mentioned in the project TODO
- Add routing (react-router) for dashboard vs. form views
- Consider pagination for large invoice lists
