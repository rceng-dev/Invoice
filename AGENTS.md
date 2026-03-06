# Invoice Generator — Agent Context

> This file provides the coding agent with full project context so it can operate effectively across the entire SDLC — not just writing code, but understanding requirements, architecture, team conventions, and project history.

---

## Project Overview

**Name:** Invoice Generator
**Type:** Client-side web application (SPA)
**Domain:** Small business invoicing — create, preview, and download invoices as PDF
**Stage:** Active development, MVP shipped, iterating on feature backlog
**Repo:** Single repo, no monorepo structure

---

## Tech Stack

| Layer         | Technology                          | Version   | Notes                                       |
|---------------|-------------------------------------|-----------|---------------------------------------------|
| Framework     | React                               | 17.0.2    | **Class components only** — do NOT introduce hooks |
| UI Library    | React Bootstrap                     | 2.0.0-beta.6 | Bootstrap 5.1.0 underneath               |
| Icons         | react-icons (Boxicons set)          | 4.2.0     | `BiPaperPlane`, `BiCloudDownload`, `BiTrash` |
| PDF Export    | html2canvas + jsPDF                 | 1.3.2 / 2.3.1 | Renders DOM to canvas, then to PDF      |
| File Download | file-saver                          | 2.0.5     | Browser-side file save                      |
| Build         | Create React App (react-scripts)    | 4.0.3     | Requires `--openssl-legacy-provider`        |
| Testing       | Jest + React Testing Library        | —         | Installed but **no tests written yet**      |
| State Mgmt    | Component state (setState)          | —         | No Redux, no Context API                    |
| Routing       | None                                | —         | Single-page, no react-router                |
| Backend       | None                                | —         | Fully client-side                           |

### Critical Constraints

1. **Class components only.** The entire codebase uses `React.Component`. Do NOT refactor to functional components or introduce hooks (`useState`, `useEffect`, etc.) unless explicitly requested. Match existing patterns.
2. **No TypeScript.** Plain JavaScript. Do not add `.ts` or `.tsx` files.
3. **No new state management libraries.** Keep state in component `this.state` with `this.setState()`.
4. **Bootstrap via React-Bootstrap.** Use `<Form.Control>`, `<Button>`, `<Row>`, `<Col>`, etc. Do not use raw HTML with Bootstrap classes when a React-Bootstrap component exists.

---

## Architecture

### Component Tree

```
App.js                          # Root wrapper — renders Container + InvoiceForm
└── InvoiceForm.js              # Central state container (249 lines)
    ├── InvoiceItem.js           # Line item table + "Add Item" button
    │   └── ItemRow              # Single item row (defined in same file)
    │       └── EditableField.js # Reusable input wrapper (InputGroup)
    └── InvoiceModal.js          # Preview modal + PDF export
```

### State Shape (lives in InvoiceForm)

```js
{
  isOpen: false,           // Modal visibility
  currency: '$',           // Currency symbol (not code)
  currentDate: '',
  invoiceNumber: 1,
  dateOfIssue: '',
  billTo: '', billToEmail: '', billToAddress: '',
  billFrom: '', billFromEmail: '', billFromAddress: '',
  notes: '',
  total: '0.00',
  subTotal: '0.00',
  taxRate: '',
  taxAmmount: '0.00',     // NOTE: typo "Ammount" is intentional — used everywhere
  discountRate: '',
  discountAmmount: '0.00', // NOTE: same typo — do NOT fix unless explicitly asked
  items: [{ id, name, description, price, quantity }]
}
```

### Data Flow

- All state lives in `InvoiceForm` — no lifting to App
- Props drill down: `InvoiceForm → InvoiceItem → ItemRow → EditableField`
- Callbacks drill down: `onItemizedItemEdit`, `onRowAdd`, `onRowDel`
- `handleCalculateTotal()` recalculates on every field change (nested `setState` callbacks)

### Known Technical Debt

| Issue | Location | Severity |
|-------|----------|----------|
| Direct state mutation (`splice`, `push` on `this.state.items`) | `InvoiceForm.js:51,63` | High |
| Typo: `taxAmmount` / `discountAmmount` used as state keys | Throughout | Low (cosmetic) |
| Hardcoded PDF filename `invoice-001.pdf` | `InvoiceModal.js:25` | Medium |
| `handleCalculateTotal` uses nested setState callbacks | `InvoiceForm.js:66-89` | Medium |
| `==` used instead of `===` | `InvoiceForm.js:100` | Low |
| `GenerateInvoice` is a standalone function, not a method | `InvoiceModal.js:12` | Low |
| No error handling on PDF generation | `InvoiceModal.js:13` | Medium |
| Currency symbols shared across currencies (USD/CAD/AUD/SGD all `$`) | `InvoiceForm.js:213-218` | Low |

> **Rule:** Do NOT fix technical debt unless the ticket explicitly asks for it. Brownfield discipline means respecting existing patterns.

---

## File Structure

```
invoice-generator/
├── public/
│   ├── index.html
│   ├── favicon.ico, favicon-16x16.png, favicon-32x32.png
│   ├── manifest.json
│   └── robots.txt
├── src/
│   ├── App.js                  # Root component
│   ├── App.css                 # Global styles
│   ├── index.js                # ReactDOM entry point
│   ├── index.css               # Minimal base styles
│   ├── reportWebVitals.js      # Performance monitoring
│   └── components/
│       ├── InvoiceForm.js      # Main form + all state
│       ├── InvoiceModal.js     # Preview modal + PDF generation
│       ├── InvoiceItem.js      # Item table + ItemRow
│       └── EditableField.js    # Reusable input field
├── to-do/                      # Product backlog (feature specs)
│   ├── 01-auto-save-local-storage.md
│   ├── 02-dynamic-pdf-filename.md
│   ├── ... (12 feature files)
├── skills/                     # Agent skill definitions
├── AGENTS.md                   # This file
├── package.json
└── .gitignore
```

---

## Git & Branching Strategy

See `skills/git-workflow.md` for full details.

**Quick reference:**
- `master` — production-ready code, protected
- `feature/<ticket-id>-<short-name>` — new features
- `bugfix/<ticket-id>-<short-name>` — bug fixes
- `hotfix/<ticket-id>-<short-name>` — urgent production fixes
- Always branch from `master`, always PR back to `master`

---

## Coding Conventions

### Style Rules

1. **Indentation:** 2 spaces (match existing files)
2. **Quotes:** Single quotes for JS strings, double quotes for JSX attributes
3. **Semicolons:** Optional — match the style of the file you're editing (most files omit trailing semicolons on methods)
4. **Naming:**
   - Components: PascalCase (`InvoiceForm`, `EditableField`)
   - Methods: camelCase (`handleRowDel`, `editField`)
   - State keys: camelCase (`billToEmail`, `taxRate`)
   - CSS classes: Bootstrap utility classes preferred over custom CSS
5. **Imports:** React first, then bootstrap components, then local components, then utilities

### Component Patterns

```js
// Follow this pattern for new components:
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { /* ... */ };
  }
  // Methods
  myMethod() { /* ... */ }
  // Arrow methods for event handlers that need `this`
  myHandler = (event) => { /* ... */ };
  render() {
    return ( /* JSX */ );
  }
}
export default MyComponent;
```

### What NOT to Do

- Do not use React hooks (`useState`, `useEffect`, `useRef`, etc.)
- Do not use functional components
- Do not introduce new CSS files — use Bootstrap utility classes
- Do not add PropTypes or TypeScript
- Do not refactor working code unless the ticket says to
- Do not fix the `taxAmmount` typo unless explicitly asked

---

## Running the Project

```bash
# Install dependencies
npm install

# Start dev server (http://localhost:3000)
npm start

# Build for production
npm run build

# Run tests
npm test
```

> **Note:** The `start` and `build` scripts include `NODE_OPTIONS=--openssl-legacy-provider` for Node.js 17+ compatibility. This is expected.

---

## Backlog & Tickets

The product backlog lives in `to-do/`. Each file is a feature spec with:
- Priority level
- Problem statement
- Acceptance criteria
- Technical notes

See `skills/ticket-workflow.md` for how tickets are picked up and worked on.

---

## Agent Roles

This agent operates across the full SDLC:

| Role | What the agent does | Relevant skill |
|------|-------------------|----------------|
| **Meeting Notetaker** | Extracts decisions, action items, and blockers from meeting transcripts | `skills/meeting-notes.md` |
| **Product Manager** | Analyzes requirements, writes specs, prioritizes backlog | `skills/product-management.md` |
| **Architect** | Designs solutions that respect existing patterns and constraints | `skills/architecture.md` |
| **Developer** | Implements features, fixes bugs, writes code in brownfield style | `skills/development.md` |
| **Code Reviewer** | Reviews PRs for quality, consistency, and adherence to conventions | `skills/code-review.md` |
| **QA** | Identifies edge cases, writes test scenarios, validates acceptance criteria | `skills/qa-testing.md` |
