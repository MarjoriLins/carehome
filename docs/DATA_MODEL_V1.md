---
title: CareHome — Data Model (ER) v1
version: 1.0
status: draft
tags: [data-model, er, mvp]
---

# 🧩 Data Model (ER) — CareHome v1 (MVP)

This document describes the **core entities**, **key fields**, and **relationships** for CareHome v1, covering:

- household access control
- dependents (humans + pets)
- medications (catalog + usage plans)
- inventory (event-based)
- lots/expiration
- alerts & notification preferences
- health agenda (appointments/exams)
- documents + OCR text
- health conditions
- providers & clinics
- provider reviews
- assistive devices (prosthetics), components, and maintenance

> Notes:
>
> - Some fields are simplified for MVP.
> - Derived values (e.g., age, expected stock, “runs out on”) are **computed**, not stored.

---

## 👥 Access Core

### `users`

- id (PK)
- email (unique)
- password_hash
- created_at
- updated_at

### `households`

- id (PK)
- name
- created_at
- updated_at

### `memberships`

- id (PK)
- user_id (FK → users.id)
- household_id (FK → households.id)
- role (`owner` | `member`)
- created_at

---

## 🧑‍🦱🐶 Dependents

### `dependents`

- id (PK)
- household_id (FK → households.id)
- name
- type (`human` | `pet`)
- birth_date
- notes
- species (nullable)
- breed (nullable)
- weight_kg (nullable)
- deleted_at (nullable)
- created_at
- updated_at

**Derived:** age is calculated from `birth_date`.

---

## 💊 Medications (Catalog + Usage Plans)

### `medications` (catalog / “what the medication is”)

Represents the medication itself (product identity).

- id (PK)
- household_id (FK → households.id)
- brand_name
- active_ingredient (nullable)
- dose_text (nullable)
- form (tablet, capsule, ml, drops)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `medication_plans` (usage / “who uses it and how”)

Represents how a dependent uses a medication.

- id (PK)
- household_id (FK → households.id)
- dependent_id (FK → dependents.id)
- medication_id (FK → medications.id)

Usage profile:

- use_type (`daily` | `weekdays` | `cycle` | `prn` | `temporary`)
- dose_per_intake (numeric, nullable)
- intakes_per_day (numeric, nullable)
- weekdays_mask (nullable) _(bitmask or array, implementation detail)_
- cycle_on_days (nullable)
- cycle_off_days (nullable)
- start_date (nullable)
- end_date (nullable)

Control:

- min_stock (nullable)
- paused (bool)
- deleted_at (nullable)
- notes (nullable)

- created_at
- updated_at

---

## 📦 Inventory (Event-Based)

### `inventory_events`

Inventory is tracked through events, not a fixed value.

- id (PK)
- household_id (FK → households.id)
- medication_plan_id (FK → medication_plans.id)
- type (`count` | `entry` | `adjust` | `loss`)
- quantity
- event_date
- notes (nullable)
- created_by_user_id (FK → users.id)
- created_at

**Derived:**

- current stock = computed from latest count and subsequent events (or via ledger rules).
- estimated “runs out on” = computed from stock + plan consumption.

---

## 🧪 Lots and Expiration

### `medication_lots`

- id (PK)
- household_id (FK → households.id)
- medication_id (FK → medications.id)
- lot_code (nullable)
- expires_on
- notes (nullable)
- created_at

> MVP note: You can keep lots independent.  
> Later versions can link lots to inventory entry events.

---

## 🚨 Notifications and Alerts

### `notification_preferences`

- id (PK)
- household_id (FK → households.id)
- user_id (FK → users.id)
- email_enabled (bool)
- telegram_enabled (bool)
- telegram_chat_id (nullable)
- timezone (nullable)
- created_at
- updated_at

### `alerts_log`

Log of notifications that were sent (for auditing and avoiding duplicates).

- id (PK)
- household_id (FK → households.id)
- user_id (FK → users.id)
- type (e.g., `low_stock`, `running_out`, `expires_soon`, `event_reminder`)
- entity_type (e.g., `medication_plan`, `lot`, `health_event`)
- entity_id
- sent_via (`in_app` | `email` | `telegram`)
- sent_at
- payload (json, nullable)
- created_at

---

## 📅 Health Agenda (Appointments & Exams)

### `health_events`

- id (PK)
- household_id (FK → households.id)
- dependent_id (FK → dependents.id)
- type (`appointment` | `exam` | `procedure` | `follow_up` | `vaccine` | `therapy`)
- title
- status (`scheduled` | `done` | `cancelled`) _(MVP)_
- start_at
- end_at (nullable)
- clinic_id (FK → clinics.id, nullable)
- provider_id (FK → providers.id, nullable)
- requested_by_provider_id (FK → providers.id, nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `event_notes`

Dated notes per appointment/exam.

- id (PK)
- household_id (FK → households.id)
- health_event_id (FK → health_events.id)
- note_date
- content
- created_by_user_id (FK → users.id)
- deleted_at (nullable)
- created_at
- updated_at

### `event_attachments`

Files (PDF/images) uploaded for an event.

- id (PK)
- household_id (FK → households.id)
- health_event_id (FK → health_events.id)
- type (e.g., `report`, `prescription`, `image`, `other`)
- file_url
- file_name
- ocr_text (nullable)
- ocr_meta (json, nullable)
- created_at

---

## 🧬 Health Conditions

### `health_conditions`

- id (PK)
- household_id (FK → households.id)
- dependent_id (FK → dependents.id)
- name
- type (`chronic` | `temporary` | `resolved`)
- status (`active` | `controlled` | `monitoring`)
- diagnosed_on (nullable)
- provider_id (FK → providers.id, nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `condition_attachments`

- id (PK)
- household_id (FK → households.id)
- condition_id (FK → health_conditions.id)
- file_url
- file_name
- ocr_text (nullable)
- ocr_meta (json, nullable)
- created_at

---

## 👨‍⚕️🏥 Providers and Clinics

### `clinics`

- id (PK)
- household_id (FK → households.id)
- name
- type (`clinic` | `lab` | `hospital` | `vet_clinic` | `prosthetics_center`)
- address (nullable)
- phone (nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `providers`

- id (PK)
- household_id (FK → households.id)
- type (`doctor` | `vet` | `technician`)
- full_name
- license_type (nullable) _(CRM/CRMV/other)_
- license_number (nullable)
- specialty (nullable)
- clinic_id (FK → clinics.id, nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

---

## ⭐ Provider Reviews

### `provider_reviews`

- id (PK)
- household_id (FK → households.id)
- provider_id (FK → providers.id)
- health_event_id (FK → health_events.id, nullable)
- rating (1–5)
- notes (nullable)
- created_by_user_id (FK → users.id)
- deleted_at (nullable)
- created_at
- updated_at

---

## 🦿 Assistive Devices (Prosthetics)

### `devices`

- id (PK)
- household_id (FK → households.id)
- dependent_id (FK → dependents.id)
- type (e.g., transtibial prosthesis)
- side (`left` | `right`, nullable)
- acquired_on (nullable)
- supplier (nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `device_components`

- id (PK)
- household_id (FK → households.id)
- device_id (FK → devices.id)
- name (liner, socket, foot, etc.)
- started_on (nullable)
- expected_lifetime_days (nullable)
- notes (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `device_maintenances`

- id (PK)
- household_id (FK → households.id)
- device_id (FK → devices.id)
- maintenance_date
- service_type (adjustment, replacement, inspection, cleaning, other)
- description (nullable)
- cost (nullable)
- location (nullable)
- provider_name (nullable)
- deleted_at (nullable)
- created_at
- updated_at

### `maintenance_notes`

Optional, editable notes about a maintenance entry.

- id (PK)
- household_id (FK → households.id)
- maintenance_id (FK → device_maintenances.id)
- content
- created_by_user_id (FK → users.id)
- deleted_at (nullable)
- created_at
- updated_at

### `maintenance_attachments`

- id (PK)
- household_id (FK → households.id)
- maintenance_id (FK → device_maintenances.id)
- type (`before` | `after` | `receipt` | `other`)
- file_url
- file_name
- created_at

---

## 🤖 AI / OCR (Support)

### `ai_jobs` (MVP placeholder)

- id (PK)
- household_id (FK → households.id)
- type
- status
- input_ref (json)
- output_ref (json)
- created_at
- updated_at

---

## 🔐 Global Modeling Rules

- All sensitive records include `household_id` (household isolation).
- No automated clinical decisions.
- Critical deletions use `deleted_at` (soft delete).
- Derived values (age, stock, “runs out on”) are computed, not stored.

---

## ✅ Status

**Data Model (ER) v1 for MVP** — aligned with Scope v1.  
Future changes → new ER version.
