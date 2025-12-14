---
title: CareHome — Stack Decision
status: pending
tags: [architecture, stack, decision]
---

# 🧱 Stack Decision — CareHome

Status: **⏳ Pending (Deferred Decision)**

The final technology stack for CareHome has intentionally **not** been locked yet.  
This document exists to ensure the decision is **explicitly deferred**, not forgotten.

---

## ✅ Why the decision is deferred

- Avoid premature optimization
- Allow informed choices after MVP needs are validated
- Keep the project flexible while the product shape becomes clearer
- Reduce rework caused by early assumptions

---

## 📌 Constraints and non-negotiables (v1)

- Household data isolation (multi-user, shared household)
- Authentication (email + password)
- Notifications (Email + Telegram)
- Database-backed persistence (not file-based)
- LGPD-minded basics (export/delete, least-privilege mindset)
- Developer experience: easy local setup

---

## 🧩 Stack areas to decide

### 1) Backend framework
Candidates (examples):
- FastAPI (Python)
- Django (Python)
- Node.js (NestJS / Express)

### 2) Database
Candidates:
- PostgreSQL (recommended default)
- SQLite (dev only)
- Managed Postgres later (cloud)

### 3) Auth
Candidates:
- JWT sessions (simple MVP)
- OAuth providers (future)
- Passkey (future)

### 4) Background jobs / scheduler
Candidates:
- Celery + Redis
- RQ + Redis
- APScheduler (simple MVP)

### 5) Notifications
Candidates:
- Email: SMTP provider / API provider (SendGrid, SES, etc.)
- Telegram Bot API

### 6) OCR / AI (future)
Candidates:
- Tesseract (local, basic)
- Cloud OCR provider (higher quality)
- LLM provider (summaries/extraction), with strict privacy rules

### 7) Frontend
Candidates:
- Next.js (React)
- Vite + React
- Mobile later (React Native / Flutter)

### 8) Hosting / deployment
Candidates:
- Local first (dev)
- Docker + compose
- Cloud (Render/Fly/Heroku-like) later

---

## ✅ Decision criteria (how we will choose)

- MVP speed and clarity
- Maintainability
- Cost and scaling path
- Security + privacy posture
- Community/docs maturity
- Compatibility with future “product” direction

---

## 🗓️ When to decide

We decide after Phase 1 starts (MVP skeleton), specifically once we confirm:
- API shape
- data model fit
- local dev workflow
- notification requirements (email/telegram)

---

## 📝 Decision log (fill when ready)

- Date:
- Final backend choice:
- Final database choice:
- Job scheduler:
- Notification providers:
- OCR/AI approach (if any):
- Frontend choice:
- Hosting choice:
- Rationale:
