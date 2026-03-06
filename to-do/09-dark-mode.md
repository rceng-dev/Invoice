# Dark Mode

## Priority: Nice to Have

## Problem
Only a light theme is available. Users working long sessions may prefer a dark interface.

## Solution
Add a dark mode toggle using Bootstrap's built-in dark theme support.

## Acceptance Criteria
- Toggle switch in the header/sidebar to switch between light and dark mode
- Preference persisted in localStorage
- Respects system preference (`prefers-color-scheme`) by default
- Invoice preview/PDF remains light regardless of UI theme

## Technical Notes
- Bootstrap 5 supports `data-bs-theme="dark"` attribute
- Apply theme to `<html>` or `<body>` element
- Ensure form inputs and modals are styled correctly in both modes
