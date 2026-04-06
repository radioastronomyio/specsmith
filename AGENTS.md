# Agent Instructions

## Repository Identity

SpecSmith is an outcome-driven specification methodology for agentic software development. This repo is the methodology's home: philosophy, spec format reference, canonical templates, and deeper methodology docs. It is not a toolkit, CLI, or framework. It contains no application code and no synthetic example specs.

**Scope boundaries:**

- **This repo** — Methodology documentation, spec format reference, canonical spec template, positioning
- **holdfast-roguelite-deckbuilder** — Primary case study; real specs live in that repo's `/spec` directory
- **project-template-repository** — Base scaffolding that this repo was forked from; template changes flow from there
- **Other radioastronomyio repos** — May contain their own `/spec` directories using SpecSmith methodology; those specs belong in those repos, not here

## Context Loading

Agents working on this repository should load context in this order:

1. This file (`AGENTS.md`) — Repository identity, constraints, conventions
2. `README.md` — Methodology overview, thesis, format reference
3. `spec/specsmith-spec-template.md` — The canonical spec template (the format this methodology defines)
4. `methodology/` — Deeper concept docs (granularity, composition, iteration)
5. `docs/documentation-standards/` — Templates and standards for documentation within this repo

## Architectural Constraints

- **No tooling** — This repo contains methodology and documentation only. No CLI, no scaffolding scripts, no runtime dependencies, no package manifests.
- **No synthetic examples** — Real specs live in real repos. Do not create example or demo specs in this repo. The spec template is the sole exception because it defines the format itself.
- **Specs are markdown** — The methodology is format-agnostic at its core. This repo's canonical template includes YAML frontmatter because the surrounding documentation system uses it. Frontmatter is repo-conventional, not methodology-essential.
- **Practice before theory** — Do not document patterns that have not been validated in at least one real project. The methodology emerged from practice and should continue that way.
- **Stable contract, variable precision** — The outcome-to-verification contract is the methodological invariant. Everything else (granularity, composition, frontmatter, tooling integration) is variable surface area.

## Documentation Conventions

- All Markdown files require YAML frontmatter (see `docs/documentation-standards/tagging-strategy.md`)
- New directories require an interior README (see `docs/documentation-standards/interior-readme-template.md`)
- Script files require language-appropriate headers (see `docs/documentation-standards/script-header-*.md`)
- Follow dual-audience commenting (see `docs/documentation-standards/code-commenting-dual-audience.md`)
- Follow writing style conventions (see `docs/documentation-standards/writing-style-guide.md`)

## Commit Messages

- Present tense, imperative mood
- 72-character first line limit
- Reference issues after first line

## Session Pattern

1. Load context (this file + README)
2. Work within defined scope
3. Document changes appropriately
4. Update work-logs if significant work completed
