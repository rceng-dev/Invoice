# Tech Stack Quick Reference

## React 17 (Class Components)

### Component Lifecycle (Used in This Project)

```
constructor(props)          → Initialize state
componentDidMount()         → Run after first render (used for initial calculation)
componentDidUpdate()        → Run after every re-render (NOT currently used — useful for auto-save)
render()                    → Return JSX
```

### State Management

```js
// Initialize (in constructor)
this.state = { field: 'value' };

// Update (triggers re-render)
this.setState({ field: 'newValue' });

// Update with callback (when you need state after update)
this.setState({ field: 'newValue' }, () => {
  // state is now updated
  console.log(this.state.field); // 'newValue'
});

// Update based on previous state
this.setState((prevState) => ({
  counter: prevState.counter + 1
}));
```

### Event Handling

```js
// Method binding (in constructor)
this.myMethod = this.myMethod.bind(this);

// Arrow function (auto-binds)
myMethod = (event) => {
  this.setState({ [event.target.name]: event.target.value });
};

// In JSX
<input onChange={(event) => this.myMethod(event)} />
<input onChange={this.myMethod} />  // If signature matches
```

---

## React-Bootstrap Components (Used in This Project)

```jsx
import Row from 'react-bootstrap/Row';
import Col from 'react-bootstrap/Col';
import Button from 'react-bootstrap/Button';
import Form from 'react-bootstrap/Form';
import Card from 'react-bootstrap/Card';
import Table from 'react-bootstrap/Table';
import Modal from 'react-bootstrap/Modal';
import InputGroup from 'react-bootstrap/InputGroup';

// Layout
<Row>
  <Col md={8} lg={9}>  {/* 8/12 on medium, 9/12 on large */}
  <Col md={4} lg={3}>  {/* Sidebar */}
</Row>

// Form
<Form onSubmit={this.handleSubmit}>
  <Form.Group className="mb-3">
    <Form.Label>Label</Form.Label>
    <Form.Control type="text" name="field" value={state.field} onChange={handler} required />
  </Form.Group>
  <Form.Select onChange={handler}>
    <option value="a">Option A</option>
  </Form.Select>
</Form>

// Input with prefix/suffix
<InputGroup>
  <Form.Control type="number" />
  <InputGroup.Text>%</InputGroup.Text>
</InputGroup>

// Modal
<Modal show={isOpen} onHide={closeHandler} size="lg" centered>
  {/* content */}
</Modal>

// Button
<Button variant="primary" type="submit">Submit</Button>
<Button variant="outline-primary" onClick={handler}>Action</Button>
```

---

## Bootstrap 5 Utility Classes (Commonly Used)

```
Layout:       d-flex, flex-row, flex-column, align-items-center, justify-content-between
Spacing:      m-2, mt-3, mb-4, p-4, px-2, py-3 (margin/padding: 0-5 scale)
Text:         fw-bold, text-secondary, text-end, text-center, small
Background:   bg-light, bg-white
Border:       border, border-2, rounded, rounded-circle
Width:        w-100, d-block
Responsive:   d-block d-md-flex, mt-3 mt-md-0
Position:     sticky-top
```

---

## jsPDF + html2canvas (PDF Generation)

```js
import html2canvas from 'html2canvas';
import jsPDF from 'jspdf';

// Capture DOM element as image, then add to PDF
html2canvas(document.querySelector("#invoiceCapture")).then((canvas) => {
  const imgData = canvas.toDataURL('image/png', 1.0);
  const pdf = new jsPDF({
    orientation: 'portrait',
    unit: 'pt',
    format: [612, 792]  // US Letter size in points
  });
  pdf.internal.scaleFactor = 1;
  const imgProps = pdf.getImageProperties(imgData);
  const pdfWidth = pdf.internal.pageSize.getWidth();
  const pdfHeight = (imgProps.height * pdfWidth) / imgProps.width;
  pdf.addImage(imgData, 'PNG', 0, 0, pdfWidth, pdfHeight);
  pdf.save('filename.pdf');
});
```

**Limitations:**
- Only captures what's visible in the DOM
- CSS gradients, shadows, and transforms may not render
- Images must be loaded before capture
- No multi-page support in current implementation

---

## react-icons (Boxicons)

```jsx
import { BiPaperPlane, BiCloudDownload, BiTrash } from "react-icons/bi";

// Usage with inline sizing
<BiPaperPlane style={{width: '15px', height: '15px', marginTop: '-3px'}} className="me-2" />
```

Browse available icons: All icons prefixed with `Bi` are from the Boxicons set.

---

## file-saver

```js
import { saveAs } from 'file-saver';

// Save a blob as a file download
saveAs(blob, 'filename.ext');
```

Currently not directly used — jsPDF's `save()` handles downloads. Available if needed for other file types.

---

## Package Scripts

```json
{
  "start": "set NODE_OPTIONS=--openssl-legacy-provider && react-scripts start",
  "build": "set NODE_OPTIONS=--openssl-legacy-provider && react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject"
}
```

The `--openssl-legacy-provider` flag is required for Node.js 17+ compatibility with webpack in CRA 4.
