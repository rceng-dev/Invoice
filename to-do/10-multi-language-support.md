# Multi-language Support (i18n)

## Priority: Nice to Have

## Problem
All invoice labels are in English. International users need invoices in their local language.

## Solution
Add internationalization support so invoice labels can be translated.

## Acceptance Criteria
- Language selector in the sidebar
- At minimum support: English, Spanish, French, German, Japanese, Chinese
- Invoice labels translated: "Bill To", "Due Date", "Amount Due", "Subtotal", etc.
- Form UI labels translated
- PDF export uses the selected language

## Technical Notes
- Use `react-i18next` or a similar i18n library
- Store translations in JSON files per locale
- Language preference persisted in localStorage
