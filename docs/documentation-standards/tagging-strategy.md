<!--
---
title: "Tagging Strategy Guide"
description: "Controlled vocabulary for document classification in specsmith"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-04-06"
version: "1.0"
tags:
  - type: guide
  - domain: documentation
related_documents:
  - "[Interior README Template](interior-readme-template.md)"
  - "[General KB Template](general-kb-template.md)"
  - "[Worklog README Template](worklog-readme-template.md)"
---
-->

# Tagging Strategy Guide

## 1. Purpose

Controlled tag vocabulary for the specsmith repository. Consistent tagging enables human navigation, RAG retrieval, and agent context loading across the repo.

---

## 2. Why Controlled Vocabulary

Uncontrolled tagging leads to synonyms fragmenting search (`spec` vs `specification` vs `specs`), inconsistent granularity (`methodology` vs `spec-format`), and tag proliferation that reduces signal. A controlled vocabulary defines allowed values upfront, ensuring consistency across contributors and time.

---

## 3. Tag Categories

Each category answers a different question about the document. Keep categories orthogonal.

| Category | Question Answered | Required |
|----------|-------------------|----------|
| `type` | What kind of document is this? | Yes |
| `domain` | What subject area? | Yes |
| `status` | What's the lifecycle state? | Recommended |

---

## 4. Domain Tags

Project-specific vocabulary for specsmith content areas.

| Tag | Boundary |
|-----|----------|
| `methodology` | Core SpecSmith concepts: outcome-driven specs, the contract model, granularity, composition, iteration |
| `case-study` | Real-world project examples demonstrating the methodology in practice |
| `positioning` | Competitive analysis, differentiation from other SDD tools, accessibility argument |
| `spec-format` | The spec template itself, format reference, canonical vs. minimum form |
| `documentation` | Templates, standards, tagging, meta-content about the repo |

### Boundary Rules

- If a document spans two domains, use the primary one. Multi-value only when genuinely split.
- `methodology` vs `spec-format`: methodology is the conceptual framework; spec-format is the concrete template and its conventions.
- `methodology` vs `positioning`: methodology describes what SpecSmith is; positioning describes what it is not and why the alternatives differ.
- `case-study` documents should reference the project repo, not duplicate its content.

---

## 5. Type Tags

| Tag | Use For |
|-----|---------|
| `project-root` | Repository root README |
| `directory-readme` | Interior README for any directory |
| `worklog` | Work log entries and milestone documentation |
| `guide` | Step-by-step procedures and how-to documents |
| `reference` | Lookup information: format specs, tag vocabularies |
| `specification` | The spec template and any meta-specs about the methodology itself |
| `report` | Analysis, findings, case study writeups |

---

## 6. Status Tags

| Tag | Description |
|-----|-------------|
| `draft` | In development, not yet complete |
| `active` | Current, maintained, approved |
| `under-review` | Scheduled or triggered review in progress |
| `deprecated` | Superseded, avoid for new work |
| `archived` | Historical reference only |

---

## 7. Implementation

### Standard Frontmatter

```yaml
<!--
---
title: "Document Title"
description: "What this document covers"
author: "VintageDon (https://github.com/vintagedon/)"
date: "YYYY-MM-DD"
version: "1.0"
status: "Active"
tags:
  - type: guide
  - domain: methodology
related_documents:
  - "[Related Doc](path/to/doc.md)"
---
-->
```

### Conventions

- Use lowercase, hyphenated values (`spec-format` not `SpecFormat` or `spec_format`)
- One value per line for readability, or array syntax for multi-value
- `related_documents` links use relative paths within the repo

---

## 8. Maintaining the Vocabulary

### Adding New Tags

1. Check if an existing tag covers the concept
2. If not, add the new tag with a boundary definition to this document
3. Backfill existing documents if the new tag applies retroactively

### Governance

- This document is the authoritative source for allowed tag values
- Prefer broader tags over proliferating specific ones
- Review additions for overlap with existing tags

---

## 9. References

| Resource | Description |
|----------|-------------|
| [Interior README Template](interior-readme-template.md) | Shows tag usage in directory READMEs |
| [General KB Template](general-kb-template.md) | Shows tag usage for standalone docs |
| [Worklog README Template](worklog-readme-template.md) | Shows tag usage for work log entries |
