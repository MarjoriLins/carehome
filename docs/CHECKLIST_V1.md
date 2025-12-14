---
title: CareHome — Checklist v1
version: 1.0
status: active
tags: [checklist, roadmap, phase-0]
---

# ✅ CareHome — Checklist v1

This checklist organizes the project into phases.  
Phase 0 is about **clarity before code**: scope, data model, and working standards.

---

## 🔷 Phase 0 — Planning & Foundation (Clarity before code)

### 🎯 Goal

Build a solid foundation before implementation:

- documented scope
- documented data model
- professional Git workflow and standards
- initial project structure

### ✅ Checklist

- [x] Define project name (CareHome)
- [x] Create Scope v1 (`docs/SCOPE_V1.md`)
- [x] Freeze Scope v1 (changes require a new version)
- [x] Create Data Model (ER) v1 (`docs/DATA_MODEL_V1.md`)
- [x] Define commit convention (`docs/COMMIT_CONVENTION.md`)
- [x] Create initial project structure (`backend/`, `frontend/`, `scripts/`, `docs/`)
- [x] Add stack decision placeholder with deferred choices documented (`docs/STACK_DECISION.md`)

### 📦 Deliverables

- `docs/SCOPE_V1.md`
- `docs/DATA_MODEL_V1.md`
- `docs/COMMIT_CONVENTION.md`
- `docs/STACK_DECISION.md`
- (optional) `docs/GIT_SETUP.md`

### ✅ Exit Criteria (Phase 0 Done)

Phase 0 is considered complete when:

- scope is versioned and stable
- ER/data model is documented
- repo has a clean structure
- basic engineering standards are documented (commits + workflow)
- stack decision is explicitly deferred (not forgotten)

---

## 🔶 Phase 1 — MVP Skeleton (next)

> Not started yet.

Planned outcomes:

- backend running locally (API skeleton + DB connection)
- basic auth and household isolation
- minimal front-end shell (navigation + login placeholder)
- development environment documented

---

## 🔶 Phase 2 — MVP Features (next)

> Not started yet.

Planned outcomes:

- dependents (humans + pets)
- medications + usage plans
- inventory events + “runs out on” calculation
- alerts (email + telegram) foundation

---

## 🔶 Phase 3 — Health Agenda & Documents (next)

> Not started yet.

Planned outcomes:

- appointments/exams
- attachments (PDF/images)
- OCR pipeline v1 (optional, based on timeline)

---

## 🔶 Phase 4 — Prices & Monitoring (future)

> Not started yet.

Planned outcomes:

- manual price tracking
- scheduled price monitoring (opt-in)
- pharmacy ranking (based on tracked data)
- optional news integration (future decision)

---

## 🔶 Phase 5 — AI Enhancements (future)

> Not started yet.

Planned outcomes:

- OCR → structured extraction
- summaries
- search/RAG on documents
- anomaly detection (non-clinical)
- all AI outputs require user confirmation
