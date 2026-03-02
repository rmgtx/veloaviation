# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Veo Aviation Email Triage Dashboard** — an AI-powered email triage and quote request automation system with a human-in-the-loop dashboard for Velo Aviation (aircraft parts/services).

### Problem

Velo Aviation receives RFQs (Requests for Quotation) from Air Exchange, ILS, and email. Currently triaged by AI agents but cannot auto-respond because:
- Pricing is manual and flexible (no fixed part pricing; changes daily based on market dynamics)
- Internal stakeholder (Greg) requires human approval on all outgoing quotes
- ERP system (Quantum Control, hosted on AWS) has limited API access — read-only as of early 2026, no write-back for quote entry
- Air Exchange and ILS platforms are heavily restricted (no public APIs, 2FA challenges)

### Target Architecture

```
Email Trigger (Outlook API / Air Exchange)
        ↓
   N8N Automation Workflow
        ↓
   RAG Agent (Email Classification)
        ├── "Yes Response" → Auto-respond
        ├── "No Response" → Auto-respond
        └── "Quote Required" ↓
                ↓
        Quantum Control API (fetch price history, SKU data)
                ↓
        Generate Quote Proposal
                ↓
        Dashboard (Human Review) — approve/reject/edit with toggle
                ↓
        Send Email + Log Transaction
```

## Planned Tech Stack

| Layer | Technology |
|-------|-----------|
| Workflow Automation | N8N (backbone for triggers, classification routing, transaction logging) |
| AI Classification | RAG agent (email classification into yes/no/quote-required) |
| ERP Integration | Quantum Control APIs (price history, SKU lookup) |
| Frontend Dashboard | Simple web UI for quote review — approve/reject/toggle workflow |
| Email Integration | Microsoft Outlook API (trigger + send) |
| Hosting | Mac Mini (runs existing OpenClaw agents) |
| Fallback Access | Headless browser automation for restricted platforms |

## Project Status

**Phase: Discovery/Planning** — no source code yet. Only a meeting transcript exists (`AI Chat - 2026_03_02 14_58 CST - Notes by Gemini.md`).

### Pending Prerequisites

- API availability assessment for Quantum Control (check if write-back APIs are now available)
- API availability assessment for Air Exchange
- Dashboard design decisions (framework, hosting)
- N8N workflow design

## Key Constraints

- **Courtesy project** — keep scope minimal, favor quick execution over polish
- **MVP-first approach** — dashboard can be "super ugly" initially; simple list with approve/reject
- **Human-in-the-loop is non-negotiable** — Greg must manually approve all outgoing quotes
- **Transaction logging required** — full audit trail of every AI-generated proposal and approval/rejection via N8N
- **Existing agent infrastructure** — 4 OpenClaw agents already running on Mac Mini (~$150/month token cost); new work should integrate with or complement this setup
