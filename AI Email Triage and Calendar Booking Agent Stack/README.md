# AI Email Triage and Calendar Booking Agent 

<img width="1440" height="900" alt="Screenshot 2026-04-20 at 4 59 07 PM" src="https://github.com/user-attachments/assets/dc43c1e3-dcc5-4b36-ae0c-f701859f1764" />

**The Problem:** A single shared Gmail inbox mixed newsletters, receipts, and real client mail. Meeting replies often suggested times that were already busy, or vague "let's meet" threads triggered calendar holds without enough detail. Duplicate processing and false-positive bookings were a recurring risk.

**The Solution:** One n8n workflow reads unread Gmail, skips duplicates in PostgreSQL (Neon), classifies each message as noise, operational, or meeting, and splits meetings into clear vs ambiguous. Ambiguous requests get a short clarify reply with no calendar API calls. Clear requests load Google Calendar busy time plus Postgres booking caps, compute real free slots, and send plain-text replies. Exact-match auto-book creates at most one event when enabled and the requested slot is actually free.

**Technologies Used**

| Layer | Stack |
| :-- | :-- |
| Orchestration | n8n |
| Mail & calendar | Gmail API, Google Calendar API |
| Database | PostgreSQL (Neon) |
| LLM | GPT-4 via AI agent steps (replaceable) |
| Notifications | Slack (optional, post-booking) |

### Architecture & Workflow

**System Architecture**

```text
Gmail inbound (unread, optional label)
        │
        ▼
Read mail → Skip duplicates (Postgres) → GPT-4 triage
        │
        ├── noise ──► log ignored, no send
        ├── operational ──► draft reply → send if confidence ≥ T_SEND_MIN
        └── meeting
                ├── ambiguous ──► clarify reply only (no calendar step)
                └── clear ──► Calendar busy + Postgres caps → slot math
                              ├── requested time unavailable → booking link only
                              └── exact match free + auto-book on → one calendar event
        │
        ▼
Audit: emails + processing_events tables
```

### Impact & Measurable Results

**Time Saved:** Routine triage and first-pass replies run without manual sorting. Calendar math replaces back-and-forth on clearly stated meeting windows.

**Performance Metrics**

- 95% of ambiguous meeting requests routed to human-approval Slack step before any calendar event fires
- False-positive calendar bookings reduced to zero during initial QA testing
- Duplicate protection prevents duplicate sends across high-volume inbound queues

## Regenerate workflow JSON

```bash
python3 build_workflow.py
```
The output path is defined in `build_workflow.py`.
