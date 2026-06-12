# 🤖 AI & Automation Engineering Portfolio

Welcome to my portfolio! This repository showcases production-grade autonomous systems, AI workflows, and business automation software I've developed.
My work focuses on leveraging tools like **n8n, LangChain, LLMs (Groq, OpenAI, Anthropic), and various API integrations** to replace manual processes with resilient, scalable, and intelligent workflows.

### What I build
- Workflow automation: n8n systems for inbound operations, scheduling, CRM updates, and data routing
- AI-assisted logic: LLM-driven classification, drafting, and decision support with guardrails
- Data pipelines: ingestion from unstructured sources, schema validation, dedupe, and audit logging
- API integrations: Gmail, Google Calendar, Apollo, HubSpot, Airtable, and custom REST services

---
## 📂 Projects Directory
*Below is a living index of my major automation projects. Click into any folder for full architectural documentation, workflow JSONs, and implementation guides.*

### 1. Invoice Processing & Accounts Payable Automation

**Stack:** n8n, automated document reading, Google Drive, Google Sheets, Slack, Odoo, ERPNext, Zoho Books

Manual invoice handling took ~40 minutes per invoice. I built an n8n workflow from Google Drive intake through automated document reading, validation, approval routing, and sync to Odoo, ERPNext, or Zoho Books. AI reads and structures invoice fields from PDF, JPG, PNG, and TIFF with duplicate checks and routes unclear invoices to a human.

**Key outcomes**

* Cut average invoice cycle time from ~40 minutes manual entry to under 10 minutes
* ~89% accuracy reading data from standard invoices; ~70% of clean invoices process automatically
* Approve/reject links, Slack notifications, and Google Sheets audit logs
* Reduced manual invoice handling by ~60% on clean invoices

### 2. Dental Clinic WhatsApp Patient Assistant

**Stack:** n8n, WhatsApp Business Platform (Meta), Google Calendar, clinic-approved knowledge base, JavaScript

Patients waited 2–4 hours for a first reply. I built a WhatsApp patient assistant for Prandelli Dental Clinic on n8n with live calendar sync and clinic-approved FAQ content from their docs. The bot routes messages by what the patient needs: FAQs, confirm/reschedule/cancel flows, and hands emergency or sensitive cases to reception with full thread context.

**Key outcomes**

* Cut average first response from 2–4 hours to under 45 seconds during the 90-day pilot
* ~32% self-service completion on confirm/reschedule/cancel flows and ~35% fewer routine confirmation calls
* Meta secure callback verification, duplicate message prevention, patient privacy checks, and staff takeover with bot pause
* Saved an estimated 10 staff hours/week and cut no-shows ~18% vs pre-pilot baseline

### 3. AI Email Triage and Calendar Booking Agent

**Stack:** n8n, PostgreSQL (Neon), GPT-4, Gmail API, Google Calendar API, Slack

Teams lose hours sorting inbox mail and booking meetings by hand. One n8n workflow triages inbound Gmail into noise, operational, and meeting paths. Meeting requests split into clear versus ambiguous before any calendar logic runs. Ambiguous requests route to human-approval Slack before any calendar event fires.

**Key outcomes**

* Routed 95% of ambiguous meeting requests to human approval before calendar booking
* Cut false-positive calendar bookings to zero during initial QA testing
* Duplicate-safe processing and plain-HTML outbound mail across high-volume inbound queues

### 4. AI Inbound Sales & CRM Pipeline

**Stack:** n8n, HubSpot, Apollo, GPT-4, AI agents, Slack, SerpAPI

SDRs spent 25+ minutes per lead on enrichment and CRM updates. An n8n workflow scores inbound leads, enriches company data through Apollo, runs AI research for talking points, writes HubSpot records, and alerts Slack. A safeguard blocks deal-stage moves without human verification.

**Key outcomes**

* Eliminated 25 minutes of manual SDR-style work per lead
* End-to-end lead flow from capture to CRM in under 3 minutes vs 25+ minutes manually
* Cut premature pipeline advances to zero in testing

### 5. AI-Powered Real Estate Dealflow & Due Diligence Automation

**Stack:** n8n, Python, Airtable, AI agents, Claude, Gmail API, data quality checks

Property teams waded through messy listings and manual PDF checks. An n8n workflow pulls unstructured property data from multiple sources, runs data quality checks, and writes clean rows to Airtable. An AI agent reads title PDFs and flags missing signatures or expired dates for human review.

**Key outcomes**

* >95% clean-record rate on first pass via data quality checks
* Handled pagination and API rate limits for hundreds of records per run without data loss
* Cut manual document check time by an estimated 80%

---

## 🛠 Core Competencies

**Automation & AI:** n8n · AI agents · knowledge-base Q&A · prompt engineering · automated document reading · secure callbacks · WhatsApp chatbot flows

**LLMs & AI APIs:** GPT-4 · Claude (Anthropic API) · Mistral · OpenAI API

**Languages:** Python · JavaScript · SQL

**Data & Storage:** PostgreSQL (Neon) · Supabase · Airtable · data quality checks

**Integrations & Platforms:** Gmail · Google Calendar · Google Drive · Google Sheets · HubSpot · Apollo · Odoo · ERPNext · Zoho Books · Slack · WhatsApp Business Platform (Meta) · SerpAPI · OAuth 2.0

## 📫 Contact

* **Email:** [judedivine9@gmail.com](mailto:judedivine9@gmail.com)
* **LinkedIn:**
* **X:**

If you want help with invoice processing, WhatsApp ops, sales pipelines, inbox operations, or data-heavy workflows, send me a message.

