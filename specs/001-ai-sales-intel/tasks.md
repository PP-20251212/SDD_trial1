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
	- [ ] T005a Create database schema and migrations (banks, regulations, insights, docs)
	- [ ] T005b Create developer DB setup scripts and docker-compose for local dev
	- [ ] T005c Implement DB seeding + sample data for pilot bank
	- [ ] T005d Add DB integration tests and migrations validation
- [ ] T006 Setup vector DB (Weaviate/Pinecone) or stub for embeddings
	- [ ] T006a Evaluate vendors (Weaviate, Pinecone, Milvus) and choose vendor
	- [ ] T006b Implement vector DB provisioning and access credentials
	- [ ] T006c Implement index schema and ingestion method for document embeddings
	- [ ] T006d Add tests for vector similarity queries (simple integration tests)
- [ ] T007 Setup message bus and workers (e.g., Redis/Kafka, Celery) for ingestion and processing
	- [ ] T007a Choose message bus type and standardize topic naming conventions
	- [ ] T007b Implement worker skeleton (in Celery/RQ) and example ingestion task
	- [ ] T007c Add health checks and failure retry strategy for workers
	- [ ] T007d Add integration test for worker queueing and processing
- [ ] T008 Implement secure storage and configuration for credentials and secrets
	- [ ] T008a Provision secret manager (Hashicorp/Cloud KMS) and store keys for connectors
	- [ ] T008b Implement secret rotation policy and access controls for services
	- [ ] T008c Document secret usage and dev workflows
- [ ] T009 Implement Authentication & Authorization (SSO for RM / OAuth2 service-accounts for integrations) placeholder for RM and connector access
	- [ ] T009a Configure SSO (SAML or OIDC) for RM user login and base roles
	- [ ] T009b Implement OAuth2 machine-to-machine client flow for connector auth
	- [ ] T009c Implement token refresh & secret storage for OAuth2 clients
	- [ ] T009d Add RBAC checks for endpoints and admin-only actions
- [ ] T009a Create OAuth2 service accounts and connector credentials (secure storage + rotation strategy)
	- [ ] T009a1 Create initial set of service accounts for demo connectors
	- [ ] T009a2 Implement rotation and revocation processes in dev environment
- [ ] T010 Implement logging, monitoring, and audit trail scaffold
	- [ ] T010a Implement structured logging (JSON) and log retention rules
	- [ ] T010b Integrate basic observability: Prometheus metrics + Grafana dashboard
	- [ ] T010c Implement audit trails for user actions and generated recommendations
- [ ] T011 Create data ingestion pipeline stub and connector pattern
	- [ ] T011a Implement connector templates (regulatory RSS, feed JSON, internal API)
	- [ ] T011b Implement parsing and canonicalization helpers for date, currency, names
	- [ ] T011c Add connector integration tests and sample data
- [ ] T012 Define and document data retention and PII rules (in collaboration with compliance)
	- [ ] T012a Draft retention policies per source type (regulatory, news, internal)
	- [ ] T012b Implement anonymization and PII masking utilities
	- [ ] T012c Document compliance sign-off process and review cycle

**Checkpoint**: Foundational components are ready; DB, vector store, workers, auth, and basic monitoring are functional.

---

## Phase 3: User Story 1 — AI Briefing Pack (Priority: P1) — Sprint 2

**Goal**: Provide RM ability to request/generate a consolidated Briefing Pack with evidence and recommended topics.

- [ ] T013 [US1] Create `Bank` model, and `SourceDocument` model in backend/src/models
	- [ ] T013a Define model fields and db migrations for Bank and SourceDocument
	- [ ] T013b Implement model validations (schemas) and tests
	- [ ] T013c Add sample data for pilot bank
- [ ] T014 [US1] Implement ingestion tasks: parse, tag, and normalise documents into DB
	- [ ] T014a Implement document fetcher for regulatory feed
	- [ ] T014b Implement document parser and tagging (topic, bank, regulation)
	- [ ] T014c Implement document deduplication and canonicalization rules
	- [ ] T014d Tests for ingestion pipeline (unit + integration)
- [ ] T015 [US1] Implement `briefing` service (ai/briefing_service) — accepts bank id and returns BriefingPack structure
	- [ ] T015a Service contract and data schema for BriefingPack
	- [ ] T015b Implement PoC generator using small knowledge base and templates
	- [ ] T015c Integrate evidence pointers and score aggregation
	- [ ] T015d Add service tests and contract tests
- [ ] T016 [US1] Integrate basic explainability: attach source references and scoring to BriefingPack
	- [ ] T016a Implement evidence link storage and excerpt extraction
	- [ ] T016b Implement scoring aggregation and scoring explanations
	- [ ] T016c Tests for explainability outputs
- [ ] T017 [US1] Implement `briefing` endpoint in API (POST /briefings/generate)
	- [ ] T017a Implement API endpoint and request/response schema
	- [ ] T017b Implement async job handling and status polling for long-running generation
	- [ ] T017c Add endpoint tests and contract tests
- [ ] T018 [US1] Add UI endpoint or minimal UI page for RM to request briefings (simple HTML or API-driven dashboard)
	- [ ] T018a Implement minimal UI page (form + results list)
	- [ ] T018b Add interactions to request briefing and view results
	- [ ] T018c Tests for UI flows (integration)
- [ ] T019 [US1] Add unit & integration tests for briefing generation pipeline
	- [ ] T019a Unit tests for AI/briefing_service components
	- [ ] T019b Integration tests for end-to-end pipeline (ingest -> brief)

**Acceptance**: RM requests briefing → gets complete pack with evidence and at least one recommended topic; generation time P95 < 2 min.

---

## Phase 4: Integrations & Offer Draft (Phase 1 additions) — Sprint 3

- [ ] T020 Implement ITDC catalog connector and mapping (normalize ITDC services into `OfferDraft` candidates)
	- [ ] T020a Implement connector for ITDC catalog ingestion
	- [ ] T020b Normalize ITDC service schema and persistence
	- [ ] T020c Add mapping logic from insights to ITDC services
	- [ ] T020d Tests for ITDC catalog integration
- [ ] T021 Implement CRM connector for lead sync and create/update lead for qualified opportunities
	- [ ] T021a Implement CRM connector authentication & error handling
	- [ ] T021b Implement mapping from Opportunity -> CRM lead structure
	- [ ] T021c Tests for CRM connector and mapping
- [ ] T022 Implement Calendar connector for follow-up reminders and scheduling
	- [ ] T022a Implement Calendar connector authentication (OAuth2) and mapping for events/reminders
	- [ ] T022b Implement follow-up scheduling flow and notification triggers
	- [ ] T022c Tests for calendar integration workflows
- [ ] T023 [US2] Implement Offer Draft generation basic workflow: input bank id + recommended services -> returns `OfferDraft`
	- [ ] T023a OfferDraft schema and data layer
	- [ ] T023b Implement generator using ITDC catalog and briefing inputs
	- [ ] T023c Add test coverage for Offer Draft generator
- [ ] T024 Add UI changes: show Offer Draft and allow RM to mark "ready-to-review" or edit
	- [ ] T024a UI design for Offer Draft view and editing
	- [ ] T024b Implement minimal UI and endpoints for updating status
	- [ ] T024c UI tests for Offer Draft actions
- [ ] T025 Add tests for connectors and Offer Draft generation
	- [ ] T025a Add integration tests for connectors (ITDC/CRM/Calendar)
	- [ ] T025b Add contract tests for Offer Draft endpoints

---

## Phase 5: Opportunity Intelligence (Cross-Sell Discovery) — Sprint 4

- [ ] T026 [US3] Implement trend analysis pipeline across group banks to detect repeated demand topics
	- [ ] T026a Implement data aggregation across banks and topics
	- [ ] T026b Implement trending detection algorithm (time-windowed frequency, TF-IDF, or embeddings cluster)
	- [ ] T026c Add evaluation metrics around precision/recall for suggestions
- [ ] T027 [US3] Implement scoring for cross-sell opportunities and suggested experts
	- [ ] T027a Define scoring model and thresholds for prioritization
	- [ ] T027b Implement scoring service and persistence of scores
	- [ ] T027c Add explanation and evidence for each scored opportunity
- [ ] T028 [US3] Integrate cross-sell suggestions with CRM and RM notifications
	- [ ] T028a Implement mapping from Opportunity -> CRM lead + follow-up activity
	- [ ] T028b Implement notification templates and scheduling rules
	- [ ] T028c Tests for notification and CRM sync flows
- [ ] T029 [US3] Add tests for cross-sell detection and scoring
	- [ ] T029a Unit tests for scoring logic
	- [ ] T029b Integration tests: detection -> score -> CRM lead

---

## Phase 6: Polish & Security — Sprint 5

- [ ] T030 [P] Add advanced explainability and audit reporting for recommendations
	- [ ] T030a Implement admin views for audit and evidence review
	- [ ] T030b Add recommendations change history and reason tracking
	- [ ] T030c Add export capabilities for legal/forensics
- [ ] T031 [P] Retention policy enforcement, data deletion and anonymization tasks
	- [ ] T031a Implement scheduled deletion jobs and retention enforcement
	- [ ] T031b Implement anonymization per policy and PII scrubbing
	- [ ] T031c Tests for retention enforcement and data deletion
- [ ] T032 [P] Security hardening and checks (network rules, data access review)
	- [ ] T032a Network and firewall hardening rules
	- [ ] T032b RBAC and least-privilege review for every service
	- [ ] T032c Prepare for a security audit / penetration test
- [ ] T033 [P] Performance optimization and monitoring for production readiness
	- [ ] T033a Add production-grade metrics and alerting (SLOs/SLA targets)
	- [ ] T033b Implement load tests and performance baselines
	- [ ] T033c Add autoscaling rules and capacity planning docs

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
