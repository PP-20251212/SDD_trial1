```markdown
---
description: "Task list for AI Sales Intelligence Platform — Phase 1"
---

# Tasks: AI Sales Intelligence Platform (Phase 1)

**Input**: plan.md, spec.md, research.md (when available)
**Prerequisites**: Plan agreed, compliance checklist, pilot bank details

## Phase 1: Setup (Shared Infrastructure) — Sprint 0

- [ ] T001 Create project structure (monitoring/, processing/, ai/, orchestration/, integrations/)
- [ ] T002 Initialize Python 3.11 + FastAPI skeleton repo in backend/
- [ ] T003 Configure CI pipeline for linting, tests, and security scans
- [ ] T004 Create initial repo docs: quickstart.md, README, contributing guidelines

---

## Phase 2: Foundational (Blocking Prerequisites) — Sprint 1

- [ ] T005 Setup PostgreSQL database and initial schema (bank, regulation, insight, documents)
- [ ] T006 Setup vector DB (Weaviate/Pinecone) or stub for embeddings
- [ ] T007 Setup message bus and workers (e.g., Redis/Kafka, Celery) for ingestion and processing
- [ ] T008 Implement secure storage and configuration for credentials and secrets
- [ ] T009 Implement Authentication & Authorization (SSO/ OAuth) placeholder for RM access
- [ ] T010 Implement logging, monitoring, and audit trail scaffold
- [ ] T011 Create data ingestion pipeline stub and connector pattern
- [ ] T012 Define and document data retention and PII rules (in collaboration with compliance)

**Checkpoint**: Foundational components are ready; DB, vector store, workers, auth, and basic monitoring are functional.

---

## Phase 3: User Story 1 — AI Briefing Pack (Priority: P1) — Sprint 2

**Goal**: Provide RM ability to request/generate a consolidated Briefing Pack with evidence and recommended topics.

- [ ] T013 [US1] Create `Bank` model, and `SourceDocument` model in backend/src/models
- [ ] T014 [US1] Implement ingestion tasks: parse, tag, and normalise documents into DB
- [ ] T015 [US1] Implement `briefing` service (ai/briefing_service) — accepts bank id and returns BriefingPack structure
- [ ] T016 [US1] Integrate basic explainability: attach source references and scoring to BriefingPack
- [ ] T017 [US1] Implement `briefing` endpoint in API (POST /briefings/generate)
- [ ] T018 [US1] Add UI endpoint or minimal UI page for RM to request briefings (simple HTML or API-driven dashboard)
- [ ] T019 [US1] Add unit & integration tests for briefing generation pipeline

**Acceptance**: RM requests briefing → gets complete pack with evidence and at least one recommended topic; generation time P95 < 2 min.

---

## Phase 4: Integrations & Offer Draft (Phase 1 additions) — Sprint 3

- [ ] T020 Implement ITDC catalog connector and mapping (normalize ITDC services into `OfferDraft` candidates)
- [ ] T021 Implement CRM connector for lead sync and create/update lead for qualified opportunities
- [ ] T022 Implement Calendar connector for follow-up reminders and scheduling
- [ ] T023 [US2] Implement Offer Draft generation basic workflow: input bank id + recommended services -> returns `OfferDraft`
- [ ] T024 Add UI changes: show Offer Draft and allow RM to mark "ready-to-review" or edit
- [ ] T025 Add tests for connectors and Offer Draft generation

---

## Phase 5: Opportunity Intelligence (Cross-Sell Discovery) — Sprint 4

- [ ] T026 [US3] Implement trend analysis pipeline across group banks to detect repeated demand topics
- [ ] T027 [US3] Implement scoring for cross-sell opportunities and suggested experts
- [ ] T028 [US3] Integrate cross-sell suggestions with CRM and RM notifications
- [ ] T029 [US3] Add tests for cross-sell detection and scoring

---

## Phase 6: Polish & Security — Sprint 5

- [ ] T030 [P] Add advanced explainability and audit reporting for recommendations
- [ ] T031 [P] Retention policy enforcement, data deletion and anonymization tasks
- [ ] T032 [P] Security hardening and checks (network rules, data access review)
- [ ] T033 [P] Performance optimization and monitoring for production readiness

---

## Dependencies & Execution Order

- Setup must finish before Foundational; Foundational must finish before story implementation
- Integrations can be implemented in parallel with Offer Draft work depending on team size

---

## Notes

- Keep tasks small and independently testable
- For each `Txxx`, add acceptance criteria and expected outputs as part of the ticket
- Document runbooks for ingestion and onboarding new sources

```
