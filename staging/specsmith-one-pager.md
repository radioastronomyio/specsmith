# SpecSmith

**Domain:** Spec-Driven Development Methodology
**Status:** Idea crystallized, repo scaffolding next
**Date:** 2026-04-05
**Version:** 1.3

---

## Vision

SpecSmith is an outcome-driven specification methodology for agentic software development. Specs define *what done looks like* through verifiable test gates, not *how to build it* through implementation instructions. The format is plain markdown. No CLI, no scaffolding, no runtime dependencies. A spec can originate on a napkin, a voice memo, a whiteboard, or a Google Doc, then formalize into source-controlled markdown with test criteria that any agent can build against.

> "The best programmer of the future will be the best explainer." — Sean Grove, OpenAI presentation on specification-as-code

---

## Core Concepts

### Outcome-Driven Specs

Specs define desired outcomes with verifiable success criteria. The agent determines implementation. The human determines acceptance.

```yaml
# Traditional spec (HOW)
- Install nginx
- Configure varnish cache
- Set up SSL termination

# SpecSmith spec (WHAT)
outcome: Web service responding on HTTPS with sub-20ms latency
tests:
  - curl -k https://localhost returns 200
  - p95 latency < 20ms under 100 concurrent connections
  - SSL Labs score >= A
```

### Granularity Slider

The same problem can be specced at any depth. The spec scales with the author's expertise and the project's requirements.

| Level | Spec Content | Test Complexity |
|-------|-------------|-----------------|
| L1 | "Website loads on HTTPS, latency < 20ms" | 2-3 basic assertions |
| L2 | "nginx with varnish cache, specific TLS config" | Suite of performance and config tests |
| L3 | "Framework compliance, security baseline, HA requirements" | Comprehensive test matrix with modular gate sets |

The format doesn't change between levels. The granularity of the outcome definition and the test gate set scales up. An L1 spec is still a valid, buildable, verifiable spec.

### Modular Composition

Specs can reference other specs as requirements. Write the "nginx hardened baseline" module once. Any project needing nginx references it. Update the module, every referencing project inherits updated test criteria.

This creates a library of reusable spec components: security baselines, performance standards, framework compliance checks. Institutional knowledge encoded as verifiable outcomes.

### Spec Is Code

Specs live in `/spec` directories within repos. They are source controlled, versioned, diffable, reviewable in PRs. The git history of a spec tells the story of how understanding of the problem deepened. First-pass test gates may miss edge cases. The spec evolves alongside the code it drives. That's not failure; that's the methodology working.

---

## Positioning: What SpecSmith Is Not

SpecSmith is not a toolkit, CLI, IDE plugin, or framework. It is a methodology with a reference implementation.

| Tool | What It Is | SpecSmith Difference |
|------|-----------|---------------------|
| GitHub Spec Kit | CLI + templates, rigid phase gates, Python setup | SpecSmith is just markdown. No install, no scaffolding |
| OpenSpec | Node.js package, slash commands, config YAML | SpecSmith has zero runtime dependencies |
| AWS Kiro | Full IDE fork with spec workflow baked in | SpecSmith is tool-agnostic, works with any editor/agent |
| forgespec-mcp | MCP server for contract validation | SpecSmith is a methodology, not a server |

The accessibility argument is the core differentiator: if you can write markdown, you can write a SpecSmith spec. If your agent can read markdown and run tests, it can build to a SpecSmith spec. Language-agnostic, toolchain-agnostic, platform-agnostic.

---

## Primary Case Study: Holdfast Roguelite Deckbuilder

### Why Holdfast Matters

Holdfast (`radioastronomyio/holdfast-roguelite-deckbuilder`) is SpecSmith methodology proven at scale before the methodology had a name. A browser-based roguelite deckbuilder built entirely through spec-driven agentic development across 4 milestone cycles (M1 through M3d, M4 next).

### The Domain Novice Story

The developer behind Holdfast is an infrastructure engineer, not a game developer. Didn't know what a Monte Carlo simulation was when the project started. Had only tangential experience with game development. The entire project was approached as an engineering problem, and every architectural decision that makes Holdfast structurally sound emerged from engineering instincts applied through spec-driven thinking, not game dev best practices.

Key reasoning chain that produced the architecture:

1. **"If I'm building the game loop anyway, why not record runs?"** — Observability instinct. An engineer builds monitoring from the start. This became the Monte Carlo balance simulator: the game loop records run data because that's what instrumented systems do.

2. **"Isn't the frontend just a viewport into the game? Why not separate it?"** — Separation of concerns. The simulation is authoritative; the UI is a rendering layer. Committing to a UI before validating mechanics felt like unnecessary risk.

3. **"Maybe my idea sucks and I don't want to find out after building a UI."** — Fail-fast through specs. Build the cheapest possible validation first (a simulation with test gates), prove the mechanics work, then invest in presentation.

4. **"What if players could opt-in to submitting run metrics?"** — The game becomes a data source feeding back into the spec validation loop. Real player behavior validates or challenges the Monte Carlo predictions. The simulation says "balanced strategy wins at 51.3%"; real player data confirms or contradicts. The spec evolves from production evidence.

This is the strongest argument for SpecSmith: a non-expert in the domain produced a well-architected, quantitatively validated game by applying engineering thinking through specs. The methodology didn't require game dev expertise. It required the ability to explain what "done" looks like and define how to verify it. The project was "practically vibe coded" in that the methodology emerged organically from doing the work, not from following a prescribed framework.

### Honest Limitations: What SpecSmith Doesn't Do For You

SpecSmith lowers friction on specification and verification. It does not eliminate the need to understand your domain.

**The learning was real.** Building Holdfast required reading up on game theory, learning what Monte Carlo simulation actually is, understanding how to validate that balance metrics mean what you think they mean. The specs structured that learning into verifiable outcomes, but the learning itself was a prerequisite. You can't spec what you can't explain.

**The draw system miss.** Partway through development, balance metrics stopped making sense. Players were seeing their entire card deck every turn. No draw mechanic, no hand size limit, no discard pile. A core deckbuilder system was simply missing because it was never specced. Everyone (human and agents alike) assumed it would somehow get built even though it appeared nowhere in any specification. The agents didn't infer it. They built exactly what was specced, and what was specced had a hole.

**The lesson:** If it's not in the spec, it doesn't exist. Agents don't fill in gaps from domain knowledge you didn't provide. This is simultaneously the methodology's greatest strength (agents do what you say, not what they assume) and its most common failure mode (you have to actually say everything that matters). Spec gaps surface as bugs, not as helpful agent improvisation.

**The pivot was manageable.** By the time the draw system gap was discovered, the developer had enough contextual skill to write the spec, define the test gates, and integrate the new system without destabilizing existing milestones. The modular spec structure meant adding draw mechanics was adding a new spec, not rewriting existing ones. The 377 existing tests still passed; the new system slotted in alongside them. This is spec-driven pivoting: the cost of discovering a gap is writing a spec, not rearchitecting.

**Skill growth compounds.** Early specs were rougher, gaps were more frequent. As domain understanding deepened through the iterative spec-build-validate cycle, specs got tighter and gaps got rarer. The methodology creates a virtuous loop: writing specs forces you to articulate what you know, which reveals what you don't know, which drives learning, which produces better specs.

### What's There

- **377 passing tests** driven by milestone specs in `/spec`
- **Monte Carlo balance simulator** running 5000 seeds across 3 strategies (aggressive, defensive, balanced) to validate game balance quantitatively
- **Degenerate signal checklist** in the GDD with quantitative thresholds: win rate bands, upgrade dominance detection, stun loop prevention, card combo anomaly checks
- **Archived analysis reports** at each milestone boundary showing balance evolution over time
- **Multi-agent code reviews** from Codex, GLM-4.6/5/5.1, CoPilot, Macroscope, Greptile with extensive HITL fixes and PRs
- **AI deep research** sourced for design research (Gemini Deep Research; generalizable as "AI deep research" for public discussion)

### SpecSmith Relevance

The M2a spec (Resolver Engine & Combat System) exemplifies the SpecSmith pattern:
- **Outcome-driven:** "A `calculate_stat()` function that takes a base value and a list of active modifiers and returns the resolved integer value"
- **Non-negotiable constraints:** Integer-only arithmetic, fixed resolution order, pure functions, 200-turn cap
- **Implementation freedom:** Agent chooses internal structure within the constraint boundaries
- **Test gates:** Pytest suite validates every deliverable

The specs drove real agent work through real milestones with real code review pipelines. This is not a synthetic example.

### Current State

The `/spec` directory is gitignored. Un-gitignoring it is the single highest-impact action for making the SpecSmith methodology visible. The specs already exist and already worked. They just need to become public.

OpenSpec was also tried (an `/openspec` directory exists in the repo). It sits essentially empty with an archived changes directory. The plain markdown specs in `/spec` are what actually drove the project. This contrast is itself a data point for the SpecSmith thesis: simple formats win over complex tooling.

### Planned: Player Metrics Loop

Future state: browser game on Azure Static Web Apps (free tier, ~100GB bandwidth/month). Optional player consent checkbox before runs. Anonymized metrics collected and displayed on a companion site showing aggregate balance data. This closes the loop between simulation predictions and real-world player behavior, making the spec validation cycle continuous rather than pre-launch only.

---

## Lineage

### Origin

Sean Grove's OpenAI presentation on specification-as-code (2024/2025) planted the seed. The retired `spec-driven-ai` repo (Proxmox-Astronomy-Lab, July 2025) was the first attempt: outcome specifications driving agent execution. That repo tried to be the methodology, the infrastructure testbed, and the research platform simultaneously, and collapsed under its own scope.

### Evolution

Through months of practical agentic development across multiple repos (astronomy pipelines, gaming projects, infrastructure automation), the methodology refined:

- RAVGVR (Request-Analyze-Verify-Generate-Validate-Reflect) became the interaction pattern
- AGENTS.md became the single agent context file per repo
- Spec-driven prompts to coding agents (KiloCode, Claude Code) proved the approach worked
- The KC structured prompt skill formalized how specs translate to agent work units
- The pattern generalized across domains: ML pipelines, game development, infrastructure, certification prep

### Methodology Origin Story

SpecSmith was not designed top-down and then applied. It emerged from practice and was formalized after the proof existed. This is a fundamentally different origin than GitHub Spec Kit (designed as a framework), AWS Kiro (built as an IDE), or OpenSpec (shipped as a Node.js package). SpecSmith came from an engineer who applied engineering thinking to unfamiliar domains through specs, and the methodology crystallized from what worked across projects.

### Key Insight

The methodology doesn't need tooling. It needs *clarity*. The spec format is intentionally simple because the value is in the thinking that produces the spec, not the format that contains it. Complexity in the spec toolchain is friction that discourages spec writing. SpecSmith removes that friction entirely.

---

## Repo Plan

### Identity

- **Org:** radioastronomyio
- **Repo:** `specsmith` (may become `specsmith-agentic-coding` or similar)
- **License:** MIT
- **Scaffolding:** project-template-repository base, hydrated with SpecSmith-specific content

### Structure (Minimal Viable)

```
specsmith/
├── README.md              # Philosophy, format reference, granularity examples, project links
├── AGENTS.md              # Agent context for the repo itself
├── LICENSE
├── docs/
│   └── documentation-standards/
│       └── tagging-strategy.md
└── methodology/           # Deeper methodology docs, grows organically
    ├── README.md
    ├── granularity.md      # The slider concept in depth
    ├── composition.md      # Modular spec composition
    └── iteration.md        # Spec evolution, spec-as-code, the git history argument
```

### README Content

- **Why:** "Best explainer" thesis, accessibility argument, positioning against complex SDD tooling
- **What:** Outcome specs, granularity slider, modular composition, spec-as-code
- **How:** Spec format reference with inline examples (web server at L1/L2/L3)
- **Projects Using SpecSmith:** Table linking to public repos. Starts sparse, grows with work.
- Tone: practitioner-to-practitioner. Not academic, not marketing.

### What the Repo Does NOT Contain

- Example specs (real specs live in real repos)
- Tooling or CLI
- Duplicated content from project repos
- Pre-populated empty placeholder files

---

## Forward Items (Prioritized)

### 1. Un-gitignore `/spec` in Holdfast

Remove `spec/` from Holdfast's `.gitignore`. Commit existing specs. Immediate public visibility of the methodology in action. Single highest-impact action.

### 2. Scaffold SpecSmith Repo

Copy project template into `radioastronomyio/specsmith`. Write README. Link to Holdfast as primary case study. Keep it minimal.

### 3. SpecSmith Skill / Slash Command

The existing KC structured prompt skill (`/mnt/skills/user/kc-structured-prompt/`) is the closest ancestor. Rework into a SpecSmith skill that:
- Takes an idea (any granularity of input) and produces a structured spec with test gates
- Could become a slash command: `/specsmith "web server with caching and SSL"`
- Outputs markdown spec ready for `/spec` directory in target repo

Wait until several specs have been hand-written first. The skill should encode validated patterns, not theoretical ones.

### 4. Retro-Spec Other Public Repos

After Holdfast, apply to other active public repos:
- Astronomy pipeline repos
- Other gaming repos (The Beating Dark, Within Parameters, etc.)
- Any actively developed public repo

### 5. Blog Series (donaldfountain.ai Substack)

SpecSmith methodology as a blog series. Each post focuses on one concept:
- The accessibility argument (napkin to source control)
- Granularity slider with real examples from Holdfast
- Modular composition
- Spec iteration (spec is code)
- Case study: engineering game balance through Monte Carlo simulation (domain novice angle)
- The draw system miss: "if it's not in the spec, it doesn't exist"
- The OpenSpec-tried-and-abandoned story as supporting evidence
- "I practically vibe coded this": how SpecSmith emerged from practice, not theory

### 6. Website Deprioritized

The llms.donaldfountain.ai concept for agent-consumable content is deprioritized. Blog + repo + real project specs provide sufficient public surface. Revisit only if demand materializes.

---

## Decisions Log

| Decision | Rationale |
|----------|-----------|
| radioastronomyio org, not separate org | Clean enough separation from EthOps. No ethical concerns with sponsors. Avoids org sprawl. |
| ForgeSpec rejected | Name collision with existing `forgespec-mcp` in the SDD space |
| SpecSmith chosen | Communicates craft/flexibility. Smith works at a forge, implies skill and malleability. Agnostic feel. |
| No examples directory | Real specs in real repos. Avoids synthetic sandbox. Proof is in production use. |
| Minimal initial scope | README + lightweight methodology docs. Grows organically with practice. |
| Spec format is just markdown | Core differentiator. Zero dependencies. Maximum accessibility. |
| Holdfast as primary case study | 377 tests, 4 milestone cycles, Monte Carlo balance sim, multi-agent reviews. Built by a domain novice using engineering thinking through specs. |
| Un-gitignore spec/ first | Specs already exist and worked. Making them public is zero-effort, maximum-visibility. |
| Methodology emerged from practice | Not designed top-down. Formalized after proof existed across multiple domains. Different origin story than Spec Kit, Kiro, OpenSpec. |
| Include honest limitations | Draw system miss, domain learning requirements, skill growth curve. Credibility through honesty, not through overselling. |

---

## Document Info

| | |
|---|---|
| Author | CrainBramp + Claude |
| Created | 2026-04-05 |
| Updated | 2026-04-05 |
| Version | 1.3 |
| Status | Idea crystallized, awaiting repo scaffold |
| Next Action | Un-gitignore `/spec` in Holdfast, then scaffold specsmith repo |

---

## Sources

- Sean Grove, OpenAI specification-as-code presentation: https://www.youtube.com/watch?v=8rABwKRsec4
- Retired `spec-driven-ai` repo README (Proxmox-Astronomy-Lab, July 2025): uploaded to this conversation
- Holdfast repo: `D:\development-repositories\holdfast-roguelite-deckbuilder` (local), `radioastronomyio/holdfast-roguelite-deckbuilder` (GitHub)
- GitHub Spec Kit: https://github.com/github/spec-kit
- OpenSpec: https://github.com/Fission-AI/OpenSpec
- AWS Kiro: https://kiro.dev/
- Claude Project conversation, 2026-04-05: SpecSmith naming, methodology discussion, Holdfast case study analysis, domain novice narrative, honest limitations
