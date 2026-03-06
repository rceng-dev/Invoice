# Development Skill

## Brownfield Development Rules

This is a brownfield project. The agent must respect existing patterns, even imperfect ones.

### Pattern Matching Checklist

Before writing any code, verify:

- [ ] **Component style:** Using class components with `extends React.Component`?
- [ ] **State management:** Using `this.state` and `this.setState()` only?
- [ ] **UI components:** Using React-Bootstrap imports, not raw HTML?
- [ ] **Naming:** Matching existing camelCase for state/methods, PascalCase for components?
- [ ] **File location:** New components go in `src/components/`?
- [ ] **Import order:** React → Bootstrap → Local components → Utilities?

### How to Add a New Feature

1. **Read the ticket** in `to-do/` — understand acceptance criteria
2. **Read the affected files** — understand current structure before changing anything
3. **Identify the minimal change set** — touch as few files as possible
4. **Match existing patterns** — if the codebase uses `var`, don't switch to `const/let` in the same file
5. **Test manually** — run `npm start`, verify in browser, check PDF export

### How to Add a New Component

```js
// src/components/NewComponent.js
import React from 'react';
import 'bootstrap/dist/css/bootstrap.min.css';
// Import only the React-Bootstrap components you need
import Card from 'react-bootstrap/Card';

class NewComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
  }

  render() {
    return (
      <Card>
        {/* Component content */}
      </Card>
    );
  }
}

export default NewComponent;
```

### How to Add State

New state belongs in `InvoiceForm.js` constructor:

```js
constructor(props) {
  super(props);
  this.state = {
    // ... existing state
    newField: 'default',  // Add new fields here
  };
}
```

Pass down via props — do NOT create new state containers.

### How to Handle Events

Follow the existing pattern:

```js
// In InvoiceForm.js — arrow function for auto-binding
myHandler = (event) => {
  this.setState({ [event.target.name]: event.target.value });
  this.handleCalculateTotal(); // If it affects calculations
};

// In render — pass handler as prop
<ChildComponent onMyEvent={this.myHandler} />
```

### PDF Export Considerations

Any visual change to the invoice preview (`InvoiceModal.js`) must be verified in the exported PDF:

1. The preview modal content inside `#invoiceCapture` is what gets rendered to PDF
2. `html2canvas` captures the DOM as-is — dynamic content, images, and styles must be fully loaded
3. Test PDF export after every UI change to the modal
4. Keep the modal content simple — complex CSS (gradients, shadows, transforms) may not render in PDF

### Files You'll Touch Most Often

| Task | Primary file | Secondary files |
|------|-------------|-----------------|
| Add form fields | `InvoiceForm.js` | `InvoiceModal.js` (preview) |
| Add line item columns | `InvoiceItem.js` | `EditableField.js`, `InvoiceModal.js` |
| Change PDF output | `InvoiceModal.js` | — |
| Add sidebar controls | `InvoiceForm.js` (Col md={4}) | — |
| Style changes | `App.css` | Bootstrap utilities inline |

### Common Pitfalls

1. **State mutation** — The codebase has direct mutations (`this.state.items.splice()`). When adding new code, use immutable patterns (`filter`, `map`, spread). Do NOT fix existing mutations unless asked.
2. **Calculation timing** — `handleCalculateTotal()` uses nested `setState` callbacks. If your feature affects calculations, call it after your `setState` and be aware of async state updates.
3. **PDF filename** — Currently hardcoded in `InvoiceModal.js:25`. If your feature changes invoice identity, consider updating this (check ticket scope first).
