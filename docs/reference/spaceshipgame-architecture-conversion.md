---
title: "SpaceshipGame Architecture Conversion"
description: How to adapt BMGD's architecture workflow into a Copilot-friendly architecture prompt/doc flow for SpaceshipGame
---

# SpaceshipGame architecture conversion

This note defines the next concrete source-to-target conversion for the current
branch: adapting `gds-game-architecture` into a lightweight GitHub Copilot flow
for `diwad-code/SpaceshipGame`.

## Why this is the right next conversion

`gds-game-architecture` is the highest-value technical workflow in BMGD because
it turns design intent into architectural decisions that keep later AI
implementation work consistent.

That matches the current state of `SpaceshipGame`, which already has:

- approved stack rules in `.github/copilot-instructions.md`
- a durable architecture document in `docs/ARCHITECTURE.md`
- ADR support in `docs/ADRs/`
- workflow guidance in `docs/COPILOT_WORKFLOW.md`
- lightweight planner and architect agents under `.github/agents/`

What the target repo does not yet have is a dedicated Copilot-facing
architecture prompt that systematically turns game brief, GDD, scope, and
mechanics constraints into durable architecture updates.

## Source workflow shape in BMGD

The source workflow lives in:

- `src/workflows/3-technical/gds-game-architecture/SKILL.md`
- `src/workflows/3-technical/gds-game-architecture/templates/architecture-template.md`
- `src/workflows/3-technical/gds-game-architecture/checklist.md`
- `src/workflows/3-technical/gds-game-architecture/decision-catalog.yaml`
- `src/workflows/3-technical/gds-game-architecture/architecture-patterns.yaml`
- `src/workflows/3-technical/gds-game-architecture/knowledge/phaser-engine.md`
- `src/workflows/3-technical/gds-game-architecture/steps/`

Its durable value is not the BMad runtime or micro-step file control. The value
is:

- architecture as a downstream artifact from design
- explicit decision capture
- stable project structure guidance
- implementation patterns for agent consistency
- architecture-specific validation
- engine-aware guidance, especially for Phaser

## Source workflow behaviors worth preserving

The most valuable source behaviors to carry over are:

1. architecture starts from design inputs, not from raw coding
2. decisions are explicit, not implied
3. project structure and implementation patterns are documented for agents
4. the document separates system boundaries from implementation details
5. architectural constraints stay durable through ADRs and source-of-truth docs
6. engine-specific guidance is loaded only when relevant

## Target-side artifact set for SpaceshipGame

Do not port the runtime mechanics. Convert the workflow into these lightweight
target artifacts:

| Target artifact | Purpose | Priority |
| --- | --- | --- |
| `.github/prompts/architecture.prompt.md` | interactive Copilot prompt for creating, refining, or reviewing architecture decisions | High |
| `docs/ARCHITECTURE.md` | canonical durable architecture document for the target repo | High |
| `docs/ADRs/ADR-*.md` | durable records for new technical decisions or dependency changes | High |
| `docs/COPILOT_WORKFLOW.md` update | explain when to use the architecture prompt after brief/GDD/mechanika updates | High |

Optional later additions:

- `.github/agents/game-architect.agent.md` update so the architect agent
  explicitly routes users to the new architecture prompt
- a small checklist or review prompt only if the target repo later wants a
  dedicated architecture validation command

## Recommended target behavior

The target repo should not recreate BMGD's full workflow runtime with
frontmatter state tracking, step checkpoints, or output workspaces.

Instead:

- use one prompt file as the entry point
- inspect current target-side docs before asking for new decisions
- support create, refine, and review behavior from the same prompt
- update `docs/ARCHITECTURE.md` in place
- write ADRs only for durable technical decisions or new dependencies

## Source-to-target mapping

| BMGD source element | SpaceshipGame destination | Adaptation note |
| --- | --- | --- |
| `SKILL.md` architecture facilitation | `.github/prompts/architecture.prompt.md` | support create, refine, or review without BMad runtime sequencing |
| `architecture-template.md` | `docs/ARCHITECTURE.md` | preserve decision-oriented structure, but compress around the repo's existing architecture format |
| `checklist.md` | validation block inside `architecture.prompt.md` | keep as a concise review rubric instead of a standalone workflow |
| `decision-catalog.yaml` | prompt guidance and ADR prompts | preserve the idea of explicit decisions, but only keep decisions relevant to Phaser/PWA/data-driven gameplay |
| `architecture-patterns.yaml` | `docs/ARCHITECTURE.md` implementation patterns | translate into repo-specific rules for scenes, systems, data, saves, UI, and mobile layouts |
| `knowledge/phaser-engine.md` | architecture prompt guidance | reuse Phaser-specific structure, lifecycle, and performance guidance without copying generic engine examples verbatim |
| project initialization and setup sections | `docs/ARCHITECTURE.md` + ADRs | keep only repo-relevant setup and stack constraints |

## SpaceshipGame-specific adjustments

The target conversion must absorb the target repo's current rules:

- Phaser 4, TypeScript, and Vite are already approved
- delivery is browser-first and Android-through-PWA first
- Dexie and Zod are already approved core tools
- `docs/SCOPE.md` defines MVP boundaries
- `mechanika/` is the source of truth for final gameplay mechanics
- new runtime dependencies require ADRs

Because of that, the converted architecture prompt should explicitly prevent
Copilot from:

- reopening already approved stack decisions without a documented reason
- designing combat, progression, faction, or quest architecture beyond stubs
  before `mechanika/` defines the rules
- putting business logic in Phaser scenes
- treating temporary Claude notes as more authoritative than
  `docs/ARCHITECTURE.md`, ADRs, or `mechanika/`

## Interaction with design inputs

This is the most important target-side difference from the generic BMGD flow.

In `SpaceshipGame`, architecture should be derived from the target repo's
durable docs in this order:

1. `mechanika/` for final gameplay rules
2. `docs/SCOPE.md` for MVP boundaries
3. `docs/GDD.md` if present
4. `docs/GAME_BRIEF.md` if present
5. existing `docs/ARCHITECTURE.md`
6. `.github/copilot-instructions.md`

The target prompt should use these rules:

- if a mechanic is not finalized in `mechanika/`, only define the integration
  point and boundary
- if `docs/ARCHITECTURE.md` already defines a system boundary, refine it instead
  of replacing it casually
- if a change introduces a new dependency or platform decision, require an ADR
- if a design detail belongs to GDD instead of architecture, push it back to the
  design docs

## Recommended structure for `docs/ARCHITECTURE.md`

The durable target architecture should keep the strongest parts of the source
workflow, but adapt them to the repo's lighter documentation model:

1. architecture position and source-of-truth order
2. approved stack and platform strategy
3. target project structure
4. core system boundaries and responsibilities
5. data architecture and validation flow
6. save architecture and schema versioning
7. UI and scene orchestration rules
8. performance and mobile/PWA constraints
9. mechanics integration points and deferred systems
10. ADR references and change-control rules

## Recommended structure for `.github/prompts/architecture.prompt.md`

The prompt should:

1. inspect:
   - `.github/copilot-instructions.md`
   - `docs/SCOPE.md`
   - `docs/GAME_BRIEF.md` if present
   - `docs/GDD.md` if present
   - `docs/ARCHITECTURE.md`
   - `docs/ADRs/`
   - `mechanika/`
2. report what architecture decisions are already settled vs still missing
3. ask only for the missing or conflicting technical decisions
4. update `docs/ARCHITECTURE.md`
5. propose new ADRs when a durable technical decision is introduced
6. end with the next 1-3 follow-up actions, usually:
   - refine missing mechanics interfaces in `mechanika/`
   - create or update an ADR
   - start implementation with the existing scene/system prompts

## Validation expectations for the target prompt

The target prompt should preserve the spirit of the BMGD architecture checklist:

- every important technical decision is explicit
- architecture guidance is specific enough for agents to implement consistently
- file and folder boundaries are clear
- scene responsibilities and system responsibilities are separated
- save/data/mobile/PWA constraints are documented
- no unresolved placeholders remain in durable docs
- approved choices and deferred mechanics are clearly distinguished

## What not to port

Do not carry over:

- `_bmad` customization/runtime conventions
- frontmatter step tracking like `stepsCompleted`
- mandatory interactive checkpoints after every micro-step
- generic web-app decision catalog entries that do not fit the target game
- architecture sections like API contracts or authentication unless the target
  repo actually needs them
- broad engine-comparison work when the target stack is already approved

## Recommended next conversion after this one

After the target-side architecture prompt/doc package is implemented in
`SpaceshipGame`, the next highest-value source task is:

1. use `./spaceshipgame-investigate-conversion.md` to implement a lightweight
   target-side investigation prompt adapted from `gds-investigate`
