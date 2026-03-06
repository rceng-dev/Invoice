# Company Logo Upload

## Priority: High / Quick Win

## Problem
Invoices look generic without branding. Users cannot add their company logo.

## Solution
Allow users to upload a logo image that appears on the invoice header.

## Acceptance Criteria
- Upload button for logo in the invoice form
- Logo preview in the form and invoice modal
- Logo appears on the exported PDF
- Support common formats: PNG, JPG, SVG
- Max file size limit (e.g., 2MB)
- Option to remove/replace logo

## Technical Notes
- Use `FileReader` API to read uploaded image as base64
- Store logo in `localStorage` for persistence
- Add logo to invoice modal and ensure html2canvas captures it
