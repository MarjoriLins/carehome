# 🧾 Commit Convention — CareHome

This document defines the **commit message convention** used in the **CareHome** project.

The goal is to ensure:

- a clean and readable commit history
- professional standards aligned with industry practices
- long-term maintainability
- readiness for hiring, collaboration, and productization

---

## 🎯 Purpose

Commits are treated as **technical communication**.

A well-written commit history allows:

- understanding _why_ decisions were made
- easier code reviews
- safer refactoring
- professional project presentation (GitHub, portfolio, hiring)

---

## 🧠 Base Standard

CareHome follows a **simplified Conventional Commits** format:

: <short, imperative description>

Example:

docs: add scope v1

---

## 🏷️ Allowed Commit Types

### 📄 `docs`

Documentation changes only.

Examples:

docs: add scope v1
docs: document prosthetics maintenance model
docs: update git workflow documentation

---

### ✨ `feat`

A new feature or user-facing functionality.

Examples:

feat: add medication inventory events
feat: support pet dependents
feat: track prosthetics maintenance records

---

### 🐛 `fix`

Bug fixes or incorrect behavior corrections.

Examples:

fix: correct stock calculation for paused medications
fix: prevent duplicate expiration alerts

---

### 🧱 `chore`

Technical tasks, maintenance, or setup changes.

Examples:

chore: add gitignore for python and node
chore: configure branch protection rules
chore: clean unused documentation drafts

---

### ♻️ `refactor`

Code changes that improve structure without changing behavior.

Examples:

refactor: simplify inventory calculation logic
refactor: rename health condition status values

---

### 🧪 `test`

Adding or updating tests.

Examples:

test: add tests for medication usage profiles
test: improve coverage for inventory events

---

### 🎨 `style`

Formatting-only changes (no logic impact).

Examples:

style: format markdown files
style: apply lint rules

---

### ⚙️ `ci`

Changes related to CI/CD, automation, or pipelines.

Examples:

ci: add basic github actions workflow
ci: configure linting pipeline

---

## 🚫 Commit Types Not Used

The following types are intentionally avoided:

- `perf` (premature optimization)
- `build` (until build tooling exists)
- emojis in commit titles

**Reason:** keep the history simple, readable, and professional.

---

## 📝 Commit Message Rules

### ✅ Do

- Use **imperative mood**
  - `add`, not `added`
  - `fix`, not `fixed`
- Keep the title under ~72 characters
- Focus on **one logical change per commit**

### ❌ Avoid

- Vague messages:

update stuff
changes
fix bug

- Multiple unrelated changes in one commit
- Emojis in commit titles

---

## 🧾 Optional Commit Body

For complex changes, a commit body may be added.

Example:

feat: track prosthetics maintenance records

Allows registering:
• maintenance date
• service type
• provider
• cost
• attachments

This improves auditability and user trust.

---

## 🌿 Branch Naming Alignment

Commit messages must align with branch naming:

| Branch Prefix | Commit Type |
| ------------- | ----------- |
| `docs/*`      | `docs`      |
| `feat/*`      | `feat`      |
| `fix/*`       | `fix`       |
| `chore/*`     | `chore`     |

Example:

branch: docs/commit-convention
commit: docs: add commit convention

---

## 🔒 Protected Branch Policy

- Direct commits to `main` are blocked
- All changes must be merged via Pull Requests
- Commit messages must follow this convention before merge

---

## 🧠 Why This Matters

This convention ensures that:

- the project looks professional to recruiters
- future contributors can onboard easily
- changes are traceable and auditable
- the project can evolve into a real, monetizable product

---

## 📌 Status

**Active**

This convention applies to all commits starting from:

docs: add scope v1

Future changes to this document require a new commit and Pull Request.
