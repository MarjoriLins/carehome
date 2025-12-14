---
title: CareHome – Scope v1
version: 1.0
status: frozen
tags: [scope, product, health, prosthetics, pets]
---

# 🩺💊 CareHome — Scope v1

**Personal health management system for families (humans + pets) and assistive devices**

---

## 🎯 Overview

**CareHome** is a system designed to **organize, track, and analyze household health information**, covering:

- medication tracking
- inventory and expiration control
- appointments and exams
- clinical history
- doctors, clinics, and service providers
- assistive devices (e.g., prosthetics)
- document upload + OCR
- assistive AI for decision support

> ⚠️ CareHome **does not replace healthcare professionals** and **does not make clinical decisions automatically**.

---

## 👥 Users and Access

### Users

- Individual accounts (email + password)
- Password recovery

### Household

- Users belong to one or more households
- Household data is shared among members
- Roles:
  - `owner`
  - `member`

---

## 🧑‍🦱🐶 Dependents (Humans and Pets)

### Features

- Register human and pet dependents
- Pets are treated as full dependents
- Fields:
  - name
  - type (`human` / `pet`)
  - birth date (**age is calculated**)
  - notes
- Additional pet fields:
  - species
  - breed
  - weight

### Rule

- All health records are always linked to a dependent.

---

## 💊 Medications

### Medication Registry

- Brand name
- Active ingredient
- Dose (free text)
- Form (tablet, capsule, ml, drops)
- Notes

### Usage Profiles (flexible)

- Daily
- Weekdays (configurable)
- Cycles (X days on / Y days off)
- PRN / as-needed
- Temporary (start/end dates)

### Rules

- Medications can be paused
- Consumption is calculated automatically
- Estimated end date is calculated from stock and usage
- **Reversible deletion (soft delete)**:
  - removed from the UI
  - retained for a configurable period to restore in case of mistakes

---

## 📦 Medication Inventory

### Model

- Inventory is **event-based**, not a single static number
- Event types:
  - count (real count)
  - entry (purchase/refill)
  - adjustment
  - loss

### Features

- Audit: expected stock × counted stock
- Configurable minimum stock
- Proactive “buy soon” suggestion

---

## 🧪 Lots and Expiration

### Features

- Lot registration
- Expiration date tracking
- Expiration alerts (60 / 30 / 15 days)

---

## 🚨 Alerts and Notifications

### Alert Types

- Low stock
- Medication running out soon
- Lot close to expiration
- Upcoming appointment/exam

### Channels

- In-app
- Email
- Telegram

### Rules

- Per-user notification preferences
- Alert sending logs
- Duplicate alert protection

---

## 📅 Health Agenda (Appointments & Exams)

### Event Types

- Appointment
- Exam
- Procedure
- Follow-up
- Vaccine
- Therapy

### Features

- Configurable reminders
- Linked to dependent
- Linked to provider and clinic
- Export calendar (.ICS)
- Export CSV

---

## 🧪 Exams and Documents

### Features

- Upload PDFs and images
- Link documents to:
  - appointments/events
  - health conditions
- Store:
  - requesting provider
  - clinic where it was performed

### OCR

- Text extraction
- Searchable text
- Preserve original document

---

## 🧬 Health Conditions

### Features

- Condition registry
- Types:
  - chronic
  - temporary
  - resolved
- Status:
  - active
  - controlled
  - under monitoring
- Attachments (exams, reports)

### Usage

- Quick view during appointments.

---

## 👨‍⚕️🏥 Providers and Clinics

### Clinics

- Full registry
- Types:
  - clinic
  - lab
  - hospital
  - vet clinic
  - orthotics/prosthetics center
- Contacts and notes

### Providers

- Doctors
- Veterinarians
- Technical providers (prosthetics)
- Fields:
  - full name
  - professional license (CRM/CRMV/other)
  - specialty
  - primary clinic

---

## ⭐ Provider Reviews

### Features

- Rating per appointment
- Dated notes
- Editable history
- Controlled deletion

### Note

- Provider education/credentials can be recorded by the user
- The system does not automatically validate professional records.

---

## 🦿 Assistive Devices (Prosthetics and Components)

### Devices

- Device registry
- Fields:
  - type (e.g., transtibial prosthesis)
  - side (left/right)
  - acquisition date
  - supplier/location
  - general notes

### Components

- Track individual components:
  - liner
  - socket
  - knee
  - prosthetic foot
  - others
- Fields:
  - start-of-use date
  - estimated lifetime (optional)
  - notes
- Component replacement history

### Maintenance and Repairs

Each maintenance record may include:

- date
- service type (adjustment, replacement, inspection, cleaning, other)
- what was done (free text)
- cost (optional)
- location
- provider/company (optional)

#### Notes and Opinions (optional)

- Optional personal notes/opinions per maintenance entry
- Notes are:
  - optional
  - editable
  - deletable
- Each note stores:
  - date
  - author

#### Attachments

- Photos (before/after)
- Receipts and service reports

### Auditability and Trust

- Maintenance history is always available
- Changes are controlled
- Goal: reduce risk of unwanted part swaps and increase trust in services

---

## 💰 Prices & Monitoring (**FUTURE / OPTIONAL**)

### Future possibilities

- Manual and automated price tracking
- Scheduled monitoring
- Pharmacy ranking
- Price-drop alerts
- Public news about medications/labs (informational, non-clinical, with source)

> Implementation details (APIs/sources/methods) will be decided when this module starts.

---

## 🤖 Assistive AI

### Use Cases

- Assist medication registration
- Structured extraction from OCR documents
- Automatic summaries
- Smart search (RAG)
- Simple anomaly detection
- Basic consumption predictions

### Rules

- AI is **assistive, explainable, and auditable**
- No automatic clinical decisions
- Human confirmation required
- AI usage is logged

---

## 📈 Annual Summary

- Per dependent summary
- Household summary
- Year timeline
- Optional AI-written narrative summary

---

## 🔐 Security and Privacy

### Principles

- Household isolation
- Authorization by household membership
- Sensitive data protection

### LGPD (Brazil)

- Data export
- Account deletion
- Transparency of data use

---

## 📤 Export and Audit

- CSV exports
- ICS calendar export
- Document export/download
- Audit logs:
  - alerts
  - OCR
  - AI usage

---

## 🚫 Out of Scope (for now)

- Automatic diagnosis
- Medical prescription
- Official provider validation
- Direct website scraping

---

## 🧠 Project Principles

- Organization > complexity
- AI as support, not authority
- Built for real-life use
- Code and docs treated equally

---

## 📌 Status

**Scope v1 is approved and frozen.**  
Future changes → new scope version.
