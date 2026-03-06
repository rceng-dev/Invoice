# Multiple Invoice Templates

## Priority: Medium / Core Feature

## Problem
Only one invoice layout is available. Users cannot customize the look of their invoices.

## Solution
Offer 3-4 invoice templates/themes that users can choose from.

## Acceptance Criteria
- At least 3 template options (e.g., Classic, Modern, Minimal)
- Template selector in the form sidebar
- Preview updates in real-time when switching templates
- Each template has distinct layout, typography, and color scheme
- PDF export respects the selected template

## Technical Notes
- Create separate CSS modules or styled components per template
- Template selection stored in state and localStorage
- Consider a color picker for custom accent colors
