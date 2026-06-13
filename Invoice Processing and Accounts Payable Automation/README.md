## Project Overview

**The Problem:** AP teams spend ~40 minutes per invoice on manual reading, data entry, duplicate checks, and approval chasing. Scanned PDFs and image invoices add reading errors. High-value bills need human sign-off without losing audit history.

**The Solution:** One n8n workflow watches a Google Drive inbox folder, archives each file, runs automated document reading plus AI that reads and structures invoice fields, validates fields and duplicates against a Sheets audit log, routes by amount and risk tier, and syncs approved bills to Odoo, ERPNext, or Zoho Books. Managers approve or reject via one-click approval links. Slack carries alerts.

**Technologies Used**

| Layer | Stack |
| :-- | :-- |
| Orchestration | n8n |
| Intake & audit | Google Drive, Google Sheets |
| Document reading & AI | Automated document reading, vision OCR, AI field extraction |
| Notifications | Slack, approve/reject links |
| Accounting sync | Odoo, ERPNext, Zoho Books (configurable) |

### Architecture & Workflow

**System Architecture**

Data flows in one direction from intake to ERP, with a branch for human approval and a parallel exception queue.

```text
Google Drive inbox (new file)
        │
        ▼
Download → Archive folder → Document reading (PDF & images)
        ▼
AI reads invoice fields → Validation & clarity scoring
        │
        ▼
Field validation → Audit log lookup → Duplicate check → Approval tier
        │
        ├── auto-approve (low risk) ──► Transform → ERP bill create
        ├── needs approval ──► Slack link + pending approvals sheet
        │         └── approval link approve/reject ──► resume → ERP
        └── validation fail ──► Exception queue
        │
        ▼
Finalize → Audit row in Sheets → Slack status
```

### Impact & Measurable Results

**Time Saved:** Average invoice cycle time dropped from ~40 minutes manual entry to under 10 minutes.

**Performance Metrics**

- ~89% accuracy reading data from standard invoices
- ~70% of clean invoices process automatically
- ~60% reduction in manual invoice handling on clean invoices
- Sync to Odoo, ERPNext, or Zoho Books (configurable per client)
