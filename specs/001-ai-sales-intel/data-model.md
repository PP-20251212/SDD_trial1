```markdown
# Data Model: AI Sales Intelligence Platform

This document defines core entities, attributes and relationships for Phase 1.

## Entities

- Bank
  - id: UUID
  - name: string
  - group: string
  - country: string
  - financial_summary: references to aggregated metrics
  - regulatory_exposure: list of Regulation IDs or tags
  - contacts: array of contact references

- RM (Relationship Manager)
  - id: UUID
  - name: string
  - email: string
  - role, team, region
  - permissions

- SourceDocument
  - id: UUID
  - bank_id: UUID (optional, if doc linked to bank)
  - source_type: enum (regulatory, report, news, internal)
  - source_url: string
  - published_at: datetime
  - content: text (or pointer to object store)
  - metadata: publisher, author, language
  - parsed_entities: list of extracted entities (json)

- Insight
  - id: UUID
  - type: enum (regulatory-impact, trend, risk, opportunity)
  - bank_id: UUID (if applicable)
  - source_document_ids: list of SourceDocument IDs
  - confidence_score: float
  - tags: list of strings
  - created_at

- BriefingPack
  - id: UUID
  - bank_id: UUID
  - generated_by: RM id
  - generated_at: datetime
  - contents: sections (financial_summary, regulatory_mapping, suggested_topics, evidence_refs)
  - evidence_refs: list of SourceDocument id + excerpt references

- OfferDraft
  - id: UUID
  - bank_id: UUID
  - scope: text
  - estimated_cost: optionally structured
  - suggested_services: list of ITDC service IDs
  - recommended_experts: list of Expert IDs
  - generated_at: datetime
  - status: draft | ready-to-review | approved

- Opportunity
  - id: UUID
  - bank_id: UUID
  - title: text
  - reason: text
  - score: float
  - suggested_offers: list of OfferDraft ids
  - created_at

- Expert
  - id: UUID
  - name: string
  - skills: list of strings
  - availability: optional calendar sync
  - contact info

- Regulation
  - id: string
  - name: string
  - effective_date
  - affected_systems
  - region

## Relationships
- Bank 1—* SourceDocument
- Bank 1—* BriefingPack
- Bank 1—* OfferDraft
- Bank 1—* Opportunity
- BriefingPack *—* SourceDocument (evidence)
- OfferDraft *—* Expert
- Insight *—* SourceDocument

## Notes
- Use normalized references and UUIDs for all major entities
- Source documents retained in object store with pointer and small excerpt cached
- Vector DB stores embeddings per SourceDocument and per extracted Insight for similarity search

---

*Data model is a draft and should be refined during Phase 1 data-model.md development.*
```
