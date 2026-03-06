# Payment Link Integration

## Priority: Medium / Core Feature

## Problem
Clients receive a PDF invoice but have no easy way to pay online.

## Solution
Integrate Stripe or PayPal to generate a payment link embedded in the invoice.

## Acceptance Criteria
- Option to add a payment link to the invoice
- Support Stripe and/or PayPal payment links
- Payment link appears as a button/QR code on the PDF
- Auto-update invoice status to "Paid" when payment is received (via webhook)
- Support partial payments (optional)

## Technical Notes
- Use Stripe Payment Links API or PayPal.me links
- Webhook listener needed for payment confirmation
- Depends on Invoice History feature (#05) for status tracking
