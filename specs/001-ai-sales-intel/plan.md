```markdown
# Implementation Plan: AI Sales Intelligence Platform (CRM dla ITDC)

**Branch**: `001-ai-sales-intel` | **Date**: 2025-12-12 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-ai-sales-intel/spec.md`

## Summary

Transformujemy reaktywną sprzedaż w proaktywną Sales Intelligence Platformę opartą na agentach AI. MVP dostarcza: monitoring zewnętrzny, generowanie "AI Briefing Pack", drafty ofert (AI Offer Builder), oraz pierwsze mechanizmy Opportunity Intelligence i Relationship Orchestration z integracją w Phase 1 (ITDC catalog, CRM, Calendar).

## Technical Context

**Language/Version**: Python 3.11 (recommended) — lub inny backendowy stack; decyzja wymaga potwierdzenia
**Primary Dependencies**: FastAPI (API), workers (Celery/RQ), embeddings/vector DB (Weaviate/Pinecone), message bus (Kafka/RabbitMQ), PostgreSQL, Redis
**Storage**: PostgreSQL for relational data; vector DB for embeddings; object store for documents
**Testing**: pytest, integration tests, contract tests (OpenAPI)
**Target Platform**: Linux server / Cloud (AWS/Azure/GCP)
**Project Type**: Backend service(s) + optional small frontend for RM (dashboard)
**Performance Goals**: Briefing generation P95 < 2 minutes for small datasets; speculative scaling to group-level bank counts (10–100 concurrently).
**Constraints**: Compliance requirements dictate PII handling, retention, and secure integrations; initial MVP supports single region and language (PL/EN).
**Scale/Scope**: MVP targets a pilot group of 5–10 banks; Phase 2 can expand by region.

## Constitution Check

GATE: Confirm legal/compliance access to internal sources and define retention. Must pass before Phase 1 release.

## Project Structure

Decision: Web API backend (FastAPI suggested), modular microservices/responsibilities:
- `monitoring/` — source ingestion and parsing (scrapers, ingestion workers)
- `processing/` — normalisation, tagging, entity extraction
- `ai/` — brief generation, offer builder, scoring models
- `orchestration/` — notifications, calendar sync, follow-ups
- `integrations/` — connectors (CRM, ITDC catalog, Calendar)
- `backend/tests/` — contract/integration/unit tests

## Complexity Tracking

Potential complexities:
- Regulation mapping (NIS2/DORA) requires legal involvement and canonical mapping across banks
- Explainability and audit trails: each recommendation must include evidence links and rationales
- Cross-sell signals may need machine learning models and threshold tuning

## Milestones & Phases

Phase 1 (MVP): Setup + Foundational + US1 (AI Briefing Pack) + Integrations (ITDC catalog, CRM, Calendar) — targeted deliverable for a single pilot bank

Phase 2: AI Offer Builder, Opportunity Intelligence, Relationship Orchestration improvements; feedback loop & learning

Phase 3: Polish, scale to multiple banks, production hardening and full compliance

---

## Deliverables per Phase

- Phase 1 Deliverables:
  - Monitoring ingestion pipeline (critical sources + scheduled scans)
  - Normalized data model (banks, regulations, insights, documents)
  - `AI Briefing Pack` generation endpoint/service
  - Phase 1 integrations: ITDC catalog connector, CRM connector, Calendar connector
  - Minimal RM UI (simple view to request briefings and view offers)
  - Basic explainability + evidence links + logging + audit trail

- Phase 2 Deliverables:
  - AI Offer Builder service with draft offer generation
  - Cross-sell detection and suggestion engine
  - Feedback loop to learn from RM actions

---

## Risks & Mitigations

- Data access/compliance delays — Mitigation: Early legal engagement and a privacy-by-design data catalog
- High cost of continuous monitoring — Mitigation: Hybrid monitoring and thresholds for source prioritization
- Model drift / false positives — Mitigation: Feedback loop and manual validation gates

---

## Acceptance criteria (phase-level)

- Phase 1: RM can request a "Briefing Pack" and receive a complete briefing in <= 2 minutes for a small dataset; the briefing includes evidence links and at least one recommended offering topic.
- Phase 1: Integrations are functional for at least one pilot bank (ITDC catalog mapping, CRM sync for leads, Calendar reminders).

---

## Open Questions (research tasks) — to resolve before Phase 1

- Confirm list of external sources and internal data sources to monitor (public/regulatory feeds, internal repos, paid sources)
- Confirm compliance requirements for PII and retention (concrete retention periods and anonymization rules)
- Decide: vector DB vendor or managed solution (Weaviate/Pinecone) and authentication method for integrations

---

## Next Steps

1. Finalize acceptance of this plan and confirm tech stack (language, DB, vector DB) — Sprint 0 (2 days)
2. Execute Setup (Phase 1) and Foundational tasks — Sprint 1 (2 weeks)
3. Implement AI Briefing Pack endpoint & Phase 1 integrations — Sprint 2 (2 weeks)
4. Validate with pilot bank and iterate — Sprint 3 (2 weeks)

---

*Plan generated from /specs/001-ai-sales-intel/spec.md — ready for task breakdown.*
```
