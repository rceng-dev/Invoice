# Terms & Conditions

## Priority: Nice to Have

## Problem
No way to add standard payment terms or legal conditions to invoices.

## Solution
Add a terms & conditions field with common presets and custom text support.

## Acceptance Criteria
- Text area for terms & conditions in the invoice form
- Preset options: "Net 15", "Net 30", "Net 60", "Due on Receipt"
- Custom text support for specific terms
- Late fee specification (e.g., "1.5% per month")
- Terms appear at the bottom of the invoice and PDF

## Technical Notes
- Add a new field to `InvoiceForm` state
- Render conditionally in `InvoiceModal` (similar to Notes)
- Store presets as constants or in a config file
