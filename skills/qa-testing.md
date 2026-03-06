# QA & Testing Skill

## Purpose

Identify edge cases, write test scenarios, and validate that acceptance criteria are met. Ensure changes don't break existing functionality.

## Test Strategy

### Current State

- Testing libraries installed (Jest, React Testing Library) but **no tests exist yet**
- All testing is currently manual
- PDF export must be tested in browser (cannot be unit tested easily)

### Manual Testing Checklist

Run through this checklist after every change:

#### Core Functionality
- [ ] Can create an invoice with all fields filled
- [ ] Can add multiple line items
- [ ] Can delete line items (including last one — edge case)
- [ ] Subtotal, tax, discount, and total calculate correctly
- [ ] Currency symbol changes when currency is switched
- [ ] "Review Invoice" button opens the modal
- [ ] Modal shows all entered data correctly

#### PDF Export
- [ ] "Send Invoice" button generates a PDF
- [ ] "Download Copy" button generates a PDF
- [ ] PDF contains all invoice data
- [ ] PDF is readable and properly formatted
- [ ] PDF filename is correct

#### Edge Cases
- [ ] Invoice with 0 tax rate — tax row hidden in preview
- [ ] Invoice with 0 discount rate — discount row hidden in preview
- [ ] Invoice with 0.01 tax/discount — row shown correctly
- [ ] Very long item names/descriptions — no layout overflow
- [ ] Very large quantities (99999) — calculations correct
- [ ] Very high prices (999999.99) — formatting correct
- [ ] Empty notes — notes section hidden in preview
- [ ] Invoice number at minimum (1) — works correctly
- [ ] Rapid field editing — no calculation errors
- [ ] Page refresh — expected behavior (data loss or persistence depending on auto-save)

#### Responsive Layout
- [ ] Desktop (1200px+) — full layout renders correctly
- [ ] Tablet (768px-1199px) — sidebar stacks correctly
- [ ] Mobile (below 768px) — form is usable

## Test Scenarios for New Features

When a new feature is implemented, generate test scenarios covering:

### Template

```markdown
## Test Scenarios: <Feature Name>

### Happy Path
1. <Normal usage scenario that should work>
   - **Steps:** ...
   - **Expected:** ...

### Edge Cases
1. <Boundary condition or unusual input>
   - **Steps:** ...
   - **Expected:** ...

### Error Cases
1. <What happens when things go wrong>
   - **Steps:** ...
   - **Expected:** ...

### Regression
1. <Existing feature that might break>
   - **Steps:** ...
   - **Expected:** <Same behavior as before>
```

### Example: Auto-save Feature

```markdown
### Happy Path
1. Data persists across refresh
   - Steps: Fill in all fields → Refresh page
   - Expected: All fields restored with previous values

### Edge Cases
1. localStorage is full
   - Steps: Fill localStorage to quota → Edit invoice
   - Expected: App continues working, save fails silently or shows warning

2. Corrupted localStorage data
   - Steps: Manually set invalid JSON in localStorage → Load page
   - Expected: App loads with default empty state, no crash

### Regression
1. Invoice calculations still work
   - Steps: Add items, set tax/discount → Verify totals
   - Expected: Same calculation results as before auto-save was added
```

## Writing Unit Tests (Future)

When tests are added, follow these conventions:

```js
// __tests__/InvoiceForm.test.js
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import InvoiceForm from '../components/InvoiceForm';

describe('InvoiceForm', () => {
  test('calculates subtotal from line items', () => {
    // Arrange
    render(<InvoiceForm />);

    // Act
    // ... interact with form

    // Assert
    // ... verify calculation
  });
});
```

### Testing Rules
- Test file goes next to the component: `src/components/__tests__/`
- One test file per component
- Test behavior, not implementation details
- Use React Testing Library queries (`getByRole`, `getByText`, not `querySelector`)
- No snapshot tests — they break too easily and provide little value
