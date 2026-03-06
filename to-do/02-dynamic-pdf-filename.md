# Dynamic PDF Filename

## Priority: High / Quick Win

## Problem
PDF downloads are hardcoded as `invoice-001.pdf` regardless of the actual invoice number.

## Solution
Use the invoice number field to generate the PDF filename dynamically.

## Acceptance Criteria
- PDF filename reflects actual invoice number (e.g., `Invoice-42.pdf`)
- Optionally include client name (e.g., `Invoice-42-AcmeCorp.pdf`)
- Sanitize filename to remove special characters

## Technical Notes
- Update `InvoiceModal.js` where `jsPDF.save()` is called
- Replace hardcoded filename with template using state values
