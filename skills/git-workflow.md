# Git Workflow & Branching Strategy

## Branch Naming

| Type | Pattern | Example | Use when |
|------|---------|---------|----------|
| Feature | `feature/<ticket-id>-<short-name>` | `feature/01-auto-save` | Adding new functionality |
| Bugfix | `bugfix/<ticket-id>-<short-name>` | `bugfix/02-pdf-filename` | Fixing non-critical bugs |
| Hotfix | `hotfix/<description>` | `hotfix/crash-on-empty-items` | Urgent production fix |
| Chore | `chore/<description>` | `chore/update-dependencies` | Non-functional changes |

- `<ticket-id>` maps to the to-do file number (e.g., `01` = `to-do/01-auto-save-local-storage.md`)
- `<short-name>` is 2-4 words, kebab-case, describing the change

## Branch Rules

1. **Always branch from `master`** — never from another feature branch
2. **One branch per ticket** — do not combine unrelated changes
3. **Delete branches after merge** — keep the repo clean

## Commit Messages

### Format

```
<type>: <short description>

<optional body — explain WHY, not WHAT>
```

### Types

| Type | When to use |
|------|-------------|
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `refactor` | Code restructuring (no behavior change) |
| `style` | Formatting, whitespace, missing semicolons |
| `docs` | Documentation only |
| `test` | Adding or updating tests |
| `chore` | Build, config, dependency changes |

### Examples

```
feat: Add auto-save to localStorage

Save invoice form state on every field change so users
don't lose work on page refresh.
```

```
fix: Use dynamic filename for PDF export

Replace hardcoded 'invoice-001.pdf' with invoice number
from form state.
```

### Rules

- Keep the subject line under 72 characters
- Use imperative mood ("Add feature" not "Added feature")
- Do not reference ticket numbers in the subject — use the branch name for traceability
- Body is optional for obvious changes, required for non-trivial ones

## Pull Request Flow

1. Push feature branch to remote
2. Open PR against `master`
3. PR must include:
   - Summary of changes (what and why)
   - How to test
   - Screenshots for UI changes
4. At least 1 approval required before merge
5. Squash merge preferred — keeps master history clean
6. Delete branch after merge

## PR Template

See `skills/pr-template.md` for the standard PR description format.

## Example Workflow

```bash
# Start work on ticket 01
git checkout master
git pull origin master
git checkout -b feature/01-auto-save

# Make changes, commit
git add src/components/InvoiceForm.js
git commit -m "feat: Add auto-save to localStorage"

# Push and create PR
git push -u origin feature/01-auto-save
gh pr create --title "feat: Add auto-save to localStorage" --body "..."
```
