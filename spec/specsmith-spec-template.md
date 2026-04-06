<!--
---
title: "SpecSmith Spec Template"
description: "Canonical template for outcome-driven specifications using the SpecSmith methodology"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-04-06"
version: "1.0"
status: "Active"
tags:
  - type: specification
  - domain: spec-format
related_documents:
  - "[Granularity](../methodology/granularity.md)"
  - "[Composition](../methodology/composition.md)"
  - "[Iteration](../methodology/iteration.md)"
---
-->

# [Spec Title]

[1-2 sentences: What this spec covers. State the capability or system being specified, not the implementation approach.]

---

## 1. Outcome

[Define what done looks like. This is the single most important section. Write it from the perspective of someone who will accept or reject the result, not someone who will build it.]

[A good outcome statement is verifiable without reading the implementation. It describes the observable state of the world after the work is complete.]

---

## 2. Test Gates

[Each gate is a concrete verification that the outcome has been achieved. Gates should be runnable: CLI commands, test assertions, inspection steps, or documented evidence.]

| Gate | Verification |
|------|-------------|
| [What is proven] | [How it is proven] |
| [What is proven] | [How it is proven] |
| [What is proven] | [How it is proven] |

---

## 3. Constraints

[Non-negotiable boundaries the implementation must respect. Constraints define what cannot be violated, distinct from outcomes which define what must be achieved.]

- [Constraint 1]
- [Constraint 2]
- [Constraint 3]

---

## 4. Scope

**Pre-existing (do not create or modify):**

- [System, service, or artifact that already exists]

**Create:**

- [What this spec produces]

**Out of scope:**

- [What this spec explicitly does not cover]

---

## 5. Dependencies

[Other specs, modules, or external requirements this spec depends on. Remove this section if none.]

| Dependency | Relationship |
|------------|-------------|
| [Spec or module name](path) | What it provides to this spec |

---

## 6. References

| Resource | Description |
|----------|-------------|
| [Link](url) | What it provides |

---

<!--
TEMPLATE USAGE NOTES (remove when using):

## The Core Contract

SpecSmith specs are built around a stable contract: define the outcome,
define the proof. The level of specificity can range from a lightweight
build spec to a compliance-grade verification matrix, but the contract
does not change.

The outcome:test keypair is the irreducible primitive. Everything else
in this template is optional structure added as needed.

## Minimum Form vs. Canonical Form

SpecSmith has a minimum form and a canonical form.

**Minimum form:** Enough markdown to express the outcome and how to
verify it. No frontmatter required. No specific section structure.
A napkin sketch with an outcome and two test assertions is a valid
SpecSmith spec.

**Canonical form:** The template above. Includes YAML frontmatter,
numbered sections, structured test gates, explicit scope boundaries.
This is the house style used in repos that follow SpecSmith's
documentation standards.

The canonical form exists because it works well in practice, not
because the methodology demands it. Use minimum form when speed
matters and canonical form when clarity matters.

## Sections

- §1 Outcome: Always include. This is the contract. If you write
  nothing else, write this.
- §2 Test Gates: Always include. Without gates, the outcome is
  an aspiration, not a spec. If you cannot write a gate for an
  outcome, the outcome is not specific enough.
- §3 Constraints: Include when there are non-negotiable boundaries.
  "Integer-only arithmetic" is a constraint. "Returns correct
  values" is an outcome.
- §4 Scope: Include when the boundary between "touch" and "don't
  touch" needs to be explicit. Prevents agents from rebuilding
  existing systems or wandering outside the spec boundary.
- §5 Dependencies: Include when this spec references or requires
  other specs. This is how modular composition works: atomic specs
  define single capabilities, composite specs assemble them.
- §6 References: Include if external resources are cited.

## Granularity

The same problem can be specced at any depth. The format stays the
same; the precision of the outcome and the breadth of the gate set
scale up.

A lightweight spec might have one outcome sentence and two gates.
A compliance-grade spec might have a detailed outcome matrix and
dozens of gates organized into categories. Both are valid specs.
The spec can change precision without changing shape.

## Writing Good Outcomes

- Describe observable state, not implementation steps
- "Web service responds on HTTPS with sub-20ms p95 latency"
  not "Install nginx and configure SSL"
- The outcome should be meaningful to someone who does not know
  what technology will be used to achieve it

## Writing Good Test Gates

- Each gate should be independently verifiable
- Prefer runnable assertions (commands, test calls, queries)
  over subjective evaluation
- At the tighter end of the granularity slider, not every gate
  will be a CLI command. Documentary evidence, configuration
  inspection, policy conformance checks, and manual acceptance
  steps are all valid gate types.

## Writing Good Constraints

- Constraints restrict how, not what
- They exist to prevent known failure modes or enforce
  architectural decisions
- If a constraint could be restated as an outcome with a test
  gate, it probably belongs in §1/§2 instead

## What Happens When a Spec Has Gaps

If the outcome and gates omit something important, the system
will expose that omission rather than inventing around it. Agents
build what is specced. They do not fill in gaps from domain
knowledge you did not provide. This is simultaneously the
methodology's greatest strength and its most common failure mode.

Spec gaps surface as bugs, not as helpful agent improvisation.
The cost of discovering a gap is writing a spec, not rearchitecting.

## Spec Evolution

Specs are source controlled, versioned, diffable, and reviewable
in PRs. The git history of a spec tells the story of how
understanding of the problem deepened. First-pass gates may miss
edge cases. The spec evolves alongside the code it drives. That
is the methodology working, not failing.
-->
