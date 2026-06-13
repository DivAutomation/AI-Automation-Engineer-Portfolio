<img width="1440" height="900" alt="Real Est Automation" src="https://github.com/user-attachments/assets/511a1837-de04-488a-9ec0-1ec156fcfe0f" />

---

# Autonomous Real Estate Sourcing & Legal Validation Agent

This is an autonomous n8n workflow that completely automates real estate deal sourcing, AI-driven investment analysis, broker outreach, and preliminary legal document verification. 

This system acts as an autonomous acqusitions team, scraping listings, evaluating them against strict investment criteria, negotiating/requesting documents, and analyzing title documents (C of O, Governor's Consent) for authenticity and red flags using LLMs.

## 🏗 System Architecture

The workflow is built entirely in **n8n** and divided into four core phases:

### Phase 1: Data Ingestion (Scraping & Normalization)
- Recursively fetches paginated property listings from target platforms
- Uses custom JavaScript to parse raw HTML blocks, extracting robust metadata (Price, Location, Bedrooms, Property Type, URL).
- Cleans and normalizes semi-structured descriptions, filtering out marketing fluff.

### Phase 2: AI Investment Evaluation
- **Tech Stack:** LangChain Agent + Llama 3 (via Groq/OpenAI).
- Properties are evaluated by an AI Agent prompted as a Senior Investment Analyst.
- **Strict Logic:** Checks constraints including budget (₦50m - ₦350m) and prime locations (Lekki, Ikoyi, Victoria Island).
- Output is enforced strictly as JSON, returning an investment score (1-10), a recommendation (`BUY`, `WATCH`, `SKIP`), and a technical justification.

### Phase 3: Automated Outreach & Database Routing
- **Routing:** Branching logic filters out `SKIP` properties, routing them to a "Rejected Deals" Airtable base to maintain historical data.
- **Database:** Approved (`BUY`) properties are logged to the primary "Investment Criteria" Airtable base.
- **Outreach:** The system automatically drafts and sends targeted emails (via Gmail API) to the listing agent requesting legal title documents (C of O, Registered Survey, Deed of Assignment).

### Phase 4: Automated Document Verification (Legal AI)
- A webhook/schedule-triggered Gmail node monitors for incoming broker replies containing PDF attachments.
- Text is extracted from attached PDFs and passed to a highly constrained AI Legal Analyst Agent.
- The AI evaluates document authenticity, cross-references location data, and flags anomalies (missing signatures, expired dates).
- **Smart Merge Algorithm:** A custom JS node programmatically handles subset matching, connecting the asynchronous email reply back to the exact initial property row in Airtable, updating the CRM with the Document Verification results.


**The Problem:** Lagos property sourcing meant manual scraping, inconsistent record quality in spreadsheets, slow broker outreach, and hours reading title PDFs for missing signatures or expired dates.

**The Solution:** Two n8n workflows run as an autonomous acquisitions pipeline. The main flow paginates public listings, normalizes fields with data quality checks, scores each property with an AI investment analyst agent (budget ₦50M–₦350M, target neighborhoods), routes BUY/WATCH/SKIP to Airtable, and emails brokers requesting C of O, Governor's Consent, survey, and deed documents. A Gmail-triggered sub-workflow extracts PDF text, runs a stronger legal analyst agent, and merges verification results back to the correct Airtable row via subject-line matching.

**Technologies Used**

| Layer | Stack |
| :-- | :-- |
| Orchestration | n8n |
| Data | HTTP scrape, JavaScript parser, data quality checks |
| AI | AI agents, GPT-4 (screening), Claude (legal document review) |
| CRM | Airtable (Investment Criteria + Rejected Deals) |
| Comms | Gmail API |

**Workflow A: Deal flow**

```text
Schedule/manual trigger
        │
        ▼
HTTP paginated scrape (~100 listings/run)
        │
        ▼
JS parse + normalize → data quality checks
        │
        ▼
Investment analyst AI agent → score 1-10, BUY|WATCH|SKIP
        │
        ├── SKIP ──► Rejected Deals Airtable
        └── BUY/WATCH ──► Investment Criteria Airtable
                │
                ▼
        Gmail outreach (due diligence doc request)
                Outreach_Status prevents duplicate sends
```

**Workflow B: Document verification**

```text
Gmail inbound (broker reply + PDF)
        │
        ▼
PDF text extraction (per attachment)
        │
        ▼
Legal analyst agent → type, authenticity 1-10, red flags, VERIFIED|CAUTION|REJECT
        │
        ▼
Smart merge → update matched Airtable row
```

### Impact & Measurable Results

**Time Saved:** Manual document check time cut by an estimated 80%. Hundreds of records per run without data loss via pagination and retry logic.

**Performance Metrics**

- >95% clean-record rate on first pass via data quality checks
- Hundreds of records processed per run with pagination and API rate-limit handling
- Dual-agent strategy: lighter model for screening, stronger model for legal PDF review
