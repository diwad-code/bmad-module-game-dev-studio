---
title: "SpaceshipGame GDD Conversion"
description: How to adapt BMGD's GDD workflow into a Copilot-friendly design prompt/doc flow for SpaceshipGame
---

# SpaceshipGame GDD conversion

This note defines the next concrete source-to-target conversion for the current
branch: adapting `gds-gdd` into a lightweight GitHub Copilot flow for
`diwad-code/SpaceshipGame`.

## Why this is the right next conversion

`gds-gdd` is the highest-value design workflow in BMGD because it turns a broad
game idea into the primary design artifact that downstream architecture,
implementation, and review work can reuse.

That matches the current state of `SpaceshipGame`, which already has:

- project-wide Copilot instructions
- scope and architecture docs
- prompt files for scenes, systems, events, and review
- a `mechanika/` area reserved for gameplay rules

What it does not yet have is a single durable design document that ties those
pieces together into one canonical design source.

## Source workflow shape in BMGD

The source workflow lives in:

- `src/workflows/2-design/gds-gdd/SKILL.md`
- `src/workflows/2-design/gds-gdd/assets/gdd-template.md`
- `src/workflows/2-design/gds-gdd/assets/gdd-validation-checklist.md`
- `src/workflows/2-design/gds-gdd/assets/game-types.csv`
- `src/workflows/2-design/gds-gdd/assets/genre-complexity.csv`
- `src/workflows/2-design/gds-gdd/assets/game-types/`
- `src/workflows/2-design/gds-gdd/references/gdd-purpose.md`

Its durable value is not the BMad runtime structure. The value is:

- the GDD-first design posture
- the traceability chain from vision to epics
- the canonical section structure
- the genre-aware design checks
- the validation discipline that keeps the document useful downstream

## Source workflow behaviors worth preserving

The most valuable source behaviors to carry over are:

1. the GDD is the primary design artifact
2. the workflow can create, update, or validate the same design source
3. design content stays implementation-agnostic
4. mechanics are documented concretely, not as vague aspirations
5. the design should stay traceable:
   - vision
   - pillars
   - core loop
   - mechanics and systems
   - epics
6. genre expectations are made explicit instead of assumed

## Target-side artifact set for SpaceshipGame

Do not port the runtime mechanics. Convert the workflow into these lightweight
target artifacts:

| Target artifact | Purpose | Priority |
| --- | --- | --- |
| `.github/prompts/gdd.prompt.md` | interactive Copilot prompt for creating, refining, or reviewing the GDD | High |
| `docs/GDD.md` | canonical durable game design document for the target repo | High |
| `docs/EPICS.md` | high-level delivery breakdown derived from the GDD | High |
| `docs/COPILOT_WORKFLOW.md` update | explain when to use the GDD prompt relative to the brief and architecture work | High |

Optional later additions:

- `.github/agents/game-planner.agent.md` update so the planner points users to
  the GDD prompt when `docs/GDD.md` is missing or stale
- a separate review prompt only if the target repo later needs a dedicated
  design-validation command

## Recommended target behavior

The target repo should not recreate BMGD's full runtime with on-activation
hooks, workspace folders, decision logs, or external handoff wiring.

Instead:

- use one prompt file as the entry point
- let Copilot inspect existing docs before asking new questions
- support create, refine, and review behavior from the same prompt
- write or update durable docs in place
- keep the design output readable by both humans and Copilot

## Source-to-target mapping

| BMGD source element | SpaceshipGame destination | Adaptation note |
| --- | --- | --- |
| `SKILL.md` create/update/validate intent | `.github/prompts/gdd.prompt.md` | support create, refine, or review in one prompt without BMad runtime assumptions |
| `gdd-template.md` | `docs/GDD.md` | preserve the core structure, but tailor sections to a Phaser/PWA/browser-first project |
| `gdd-validation-checklist.md` | validation block inside `gdd.prompt.md` | keep as a concise review rubric rather than a separate validator workflow |
| `game-types.csv` and genre guides | prompt instructions and doc sections | reuse genre-specific thinking, but only where it fits the actual game |
| `genre-complexity.csv` | prompt caution/risk logic | use it to decide where the target prompt should demand more precision |
| GDD → epics handoff | `docs/EPICS.md` | keep a lightweight human-readable epic breakdown instead of BMad workspace files |
| `gdd-purpose.md` | prompt framing and docs guidance | preserve the idea that GDD is the design source of truth before implementation begins |

## SpaceshipGame-specific adjustments

The target conversion must absorb the target repo's current rules:

- Phaser 4, TypeScript, and Vite are already approved
- delivery is browser-first and Android-through-PWA first
- `docs/SCOPE.md` already defines MVP boundaries
- `docs/ARCHITECTURE.md` already defines technical structure
- `mechanika/` is reserved for gameplay rules that are not final yet

Because of that, the converted GDD prompt should explicitly prevent Copilot
from:

- inventing combat, progression, faction, morale, or trait rules before
  `mechanika/` defines them
- contradicting `docs/SCOPE.md`
- leaking architecture or implementation details into the GDD
- rewriting approved stack choices already captured in
  `.github/copilot-instructions.md` and `docs/ARCHITECTURE.md`

## Interaction with `mechanika/`

This is the most important target-side difference from the generic BMGD flow.

In `SpaceshipGame`, the GDD should not pretend that missing mechanics are
already settled. The target prompt should use these rules:

- if `mechanika/` already defines a rule, treat it as authoritative
- if `mechanika/` does not define a rule yet, record the design intent without
  inventing formulas
- unresolved mechanics should go into open questions, assumptions, or deferred
  sections in `docs/GDD.md`
- `docs/GDD.md` should connect high-level design to `mechanika/`, not replace it

## Recommended structure for `docs/GDD.md`

The durable target GDD should keep the source workflow's strongest sections, but
compress and adapt them to the current project:

1. executive summary
2. player fantasy, pillars, and target audience
3. core gameplay loop
4. core systems and gameplay domains
5. confirmed mechanics vs deferred mechanics
6. scene and screen design expectations
7. content structure: map, events, crew, ship, mission flow
8. presentation direction: pixel-art, UI, audio, tone
9. technical constraints relevant to design
10. out of scope, assumptions, and open questions
11. delivery slices and epic candidates

## Recommended structure for `docs/EPICS.md`

The target repo should keep the epic breakdown separate from the main GDD,
mirroring the useful part of `gds-gdd` without its runtime workspace model.

Recommended sections:

1. epic overview table
2. MVP-first epic order
3. per-epic goals
4. key stories or work slices
5. dependencies and blockers
6. deferred post-MVP epics

## Recommended structure for `.github/prompts/gdd.prompt.md`

The prompt should:

1. inspect:
   - `.github/copilot-instructions.md`
   - `docs/GAME_BRIEF.md` if present
   - `docs/SCOPE.md`
   - `docs/ARCHITECTURE.md`
   - `mechanika/`
   - existing `docs/GDD.md` and `docs/EPICS.md` if present
2. report what is already known vs still missing
3. ask only for the missing design decisions
4. produce or update `docs/GDD.md`
5. produce or update `docs/EPICS.md` when enough information exists
6. end with the next 1-3 follow-up actions, usually:
   - refine unresolved design questions
   - deepen `mechanika/`
   - deepen `docs/ARCHITECTURE.md`

## Validation expectations for the target prompt

The target prompt should preserve the spirit of the BMGD validator:

- remove fluff and marketing language
- prefer concrete design statements over vague adjectives
- keep the chain from vision to mechanics to epics intact
- keep implementation details out of the GDD
- verify that deferred mechanics are clearly marked, not silently invented
- verify that scene/system/event prompts can later read the GDD without
  ambiguity

## What not to port

Do not carry over:

- `_bmad` runtime conventions
- install-time skill resolution
- workspace folder logic like `decision-log.md`
- external handoff hooks
- headless/runtime-specific orchestration
- mandatory genre guide loading when the target repo already has narrower,
  project-specific constraints

## Recommended next conversion after this one

After the target-side GDD prompt/doc package is implemented in `SpaceshipGame`,
the next highest-value source task is:

1. use `./spaceshipgame-architecture-conversion.md` to implement the
   target-side architecture prompt/doc package adapted from
   `gds-game-architecture`
