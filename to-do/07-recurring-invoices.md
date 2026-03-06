# Recurring Invoices

## Priority: Medium / Core Feature

## Problem
Users with retainer clients must manually recreate invoices every billing cycle.

## Solution
Allow users to set up recurring invoice schedules that auto-generate invoices.

## Acceptance Criteria
- Option to mark an invoice as recurring
- Frequency options: Weekly, Bi-weekly, Monthly, Quarterly, Yearly
- Auto-increment invoice number on each recurrence
- Email notification when a recurring invoice is generated
- Ability to pause/resume/cancel recurring schedules

## Technical Notes
- Requires backend with scheduled jobs (e.g., Firebase Cloud Functions with cron)
- Depends on Invoice History feature (#05) for storage
- Depends on Email Delivery feature (#04) for notifications
