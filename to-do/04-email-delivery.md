# Email Delivery

## Priority: High

## Problem
The "Send Invoice" button just downloads a PDF. There is no way to actually email an invoice to a client.

## Solution
Integrate an email service to send invoices directly from the app.

## Acceptance Criteria
- "Send Invoice" button opens a send dialog with pre-filled recipient email
- User can add a custom message/subject
- PDF is attached to the email automatically
- Success/failure feedback shown to the user
- Email history/log (optional)

## Technical Notes
- Requires a backend service (e.g., Node.js/Express + SendGrid, Resend, or AWS SES)
- Alternative: Use `mailto:` link with pre-filled fields as a quick MVP
- Consider rate limiting to prevent abuse
