```markdown
# Research: AI Sales Intelligence Platform (CRM dla ITDC)

**Goal**: Zbiór technicznych i biznesowych otwartych pytań, rekomendacji i źródeł danych, które trzeba rozstrzygnąć przed pełną implementacją Phase 1.

## Primary research topics

1. Data sources and coverage
   - Public regulatory sources (NIS2, DORA): canonical feeds, RSS/JSON endpoints from official bodies
   - Financial reports: EDGAR / local regulators / commercial data feeds
   - News and analysis: curated feeds (Reuters, Bloomberg), alerts
   - Internal sources: ITDC knowledge base, historical inquiries, CRM data, internal NFRs
   - Paid sources/subscriptions: clarify access and contracts

2. Compliance & Data Privacy
   - Confirm retention policy and PII rules with Legal/Compliance
   - Define anonymization and masking policies for external documents
   - Confirm which fields are allowed to be stored and how to obfuscate sensitive fields

3. Monitoring/ingestion architecture
   - Hybrid approach: continuous ingesters for critical sources (regulatory endpoints) + scheduled batch jobs for news/secondary sources
   - Scraper throttling, error handling, deduplication, rate limits
   - Document storage: object store vs. DB; versioning of source documents

4. Vector store & embeddings
   - Evaluate vendors: Weaviate, Pinecone, Milvus, or managed vendor
   - Embeddings model selection: OpenAI / Llama embeddings / open-source alternatives
   - Cost/latency tradeoffs

5. Explainability & Evidence
   - For each recommendation, store pointers to evidence (source documents, excerpts) + confidence score model
   - Provide raw data and scoring to legal/compliance for audit

6. Integrations
   - ITDC catalog: canonical schema for mapping services to OfferDraft candidates
   - CRM integration model: sync leads/opportunities and update from system
   - Calendar integration: reminders and scheduling for RM (Microsoft 365 / Google Calendar)

7. Teaming & Ops
   - Define SRE/ops responsibilities for monitoring and alerting
   - Define acceptance criteria for pilot bank and success metrics

## Vendor selection checklist (shortlist)
- Evaluate Weaviate vs Pinecone vs Milvus vs managed offering (auth, pricing, latency, GCP/AWS compatibility)
- Evaluate embedding providers (OpenAI, Anthropic, open-source models)
- Evaluate existing tools for evidence extraction (spaCy, SciBERT, langchain pipelines)

## Open questions (priority)
1. Confirm the final list of in-scope sources for Phase 1 (public/regulatory + internal + paid) — Legal & Ops
2. Define retention periods per source and PII handling rules — Legal & Ops
3. Confirm preferred vector store and embedding provider (budget/performance) — Tech lead
4. Confirm authentication model and internal system integration mechanisms (SSO, service accounts) — Security/Infra

## Recommendations (immediate)
- Start with public sources (NIS2/DORA) + internal ITDC catalog + CRM connectors for pilot bank
- Use hybrid ingestion (continuous for regulation + daily for news)
- Start with an open-source embedding model for prototyping, then evaluate managed vendors for production

## Research sources and references
- European Commission (regulatory pages for NIS2, DORA)
- Bank regulators portals for financial reports
- ITDC internal catalog (to be provided)
- Cloud provider DB and vector store docs

---

*Research notes — update as Phase 0 answers arrive.*
```
