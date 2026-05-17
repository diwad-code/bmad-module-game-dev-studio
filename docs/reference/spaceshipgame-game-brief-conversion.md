---
title: "SpaceshipGame Game Brief Conversion"
description: How to adapt BMGD's game-brief workflow into a Copilot-friendly prompt/doc flow for SpaceshipGame
---

# SpaceshipGame game-brief conversion

This note defines the first concrete source-to-target conversion for the current
branch: adapting `gds-create-game-brief` into a lightweight GitHub Copilot flow
for `diwad-code/SpaceshipGame`.

## Why this is the right next conversion

`gds-create-game-brief` is the best first transfer because it creates the
highest-level product framing that later prompts can reuse:

- vision and positioning
- target audience
- core gameplay pillars
- scope and constraints
- references and differentiators
- risks, MVP boundaries, and next steps

That matches the current state of `SpaceshipGame`, which is still a prompt/doc
repository with no `src/` tree and no runnable app yet.

## Source workflow shape in BMGD

The source workflow lives in:

- `src/workflows/1-preproduction/gds-create-game-brief/SKILL.md`
- `src/workflows/1-preproduction/gds-create-game-brief/templates/game-brief-template.md`
- `src/workflows/1-preproduction/gds-create-game-brief/checklist.md`
- `src/workflows/1-preproduction/gds-create-game-brief/steps/`

Its durable value is not the BMad runtime or step-file orchestration. The value
is the discovery sequence and the document structure.

### Source discovery sequence

1. initialize and load existing context documents
2. define the game vision
3. define the target market
4. define gameplay fundamentals
5. define scope and constraints
6. define references and differentiators
7. define content, production approach, and risks
8. define MVP, success metrics, and handoff

## Target-side artifact set for SpaceshipGame

Do not port the runtime mechanics. Convert the workflow into three lightweight
target artifacts:

| Target artifact | Purpose | Priority |
| --- | --- | --- |
| `.github/prompts/game-brief.prompt.md` | interactive Copilot prompt for brief creation or refinement | High |
| `docs/GAME_BRIEF.md` | canonical durable brief used by later prompts/docs | High |
| `docs/COPILOT_WORKFLOW.md` update | explain when to run the new prompt in the session order | High |

Optional later additions:

- `.github/agents/game-planner.agent.md` update so the planner points users to
  the new brief prompt when the brief is missing
- a tiny `.github/skills/` helper only if the target repo later needs reusable
  brief scaffolding

## Recommended target behavior

The target repo should not recreate the full 8-step blocking workflow from
BMGD. Instead:

- use one prompt file as the entry point
- let Copilot inspect existing docs before asking questions
- guide the user through the same semantic sections in fewer turns
- write or update one durable `docs/GAME_BRIEF.md`
- hand off to existing prompt/doc assets after the brief is stable

## Source-to-target mapping

| BMGD source element | SpaceshipGame destination | Adaptation note |
| --- | --- | --- |
| workflow activation and context discovery | beginning of `game-brief.prompt.md` | inspect `.github/copilot-instructions.md`, `docs/ARCHITECTURE.md`, `docs/SCOPE.md`, `docs/IDEAS_LATER.md`, `mechanika/`, and existing `docs/GAME_BRIEF.md` if present |
| game vision section | `docs/GAME_BRIEF.md` | keep core concept, elevator pitch, and vision statement |
| target market section | `docs/GAME_BRIEF.md` | keep audience and market framing, but bias toward browser/PWA/mobile realities |
| game fundamentals section | `docs/GAME_BRIEF.md` | keep pillars, core loop, primary mechanics, and experience goals |
| scope and constraints section | `docs/GAME_BRIEF.md` | align with Phaser 4, TypeScript, Vite, PWA-first Android delivery, Dexie, and Zod |
| reference framework section | `docs/GAME_BRIEF.md` | keep inspirations, non-goals from inspirations, competitors, and differentiators |
| content and production section | `docs/GAME_BRIEF.md` | keep world, narrative approach, art/audio direction, production approach, and risks |
| success and handoff section | `docs/GAME_BRIEF.md` | keep MVP definition, success metrics, next actions, and open questions |
| checklist | embedded validation block in `game-brief.prompt.md` | use as a concise review rubric instead of a separate runtime checklist |

## SpaceshipGame-specific adjustments

The target conversion must absorb the repo's current rules:

- the approved stack is already fixed in `.github/copilot-instructions.md`
- the project is browser-first and Android-through-PWA first
- mechanics-dependent detail must wait for `mechanika/`
- the MVP boundary is already partially defined in `docs/SCOPE.md`
- architecture decisions already live in `docs/ARCHITECTURE.md`

Because of that, the converted prompt should explicitly prevent Copilot from:

- inventing combat, progression, faction, trait, or morale systems too early
- proposing scope that conflicts with `docs/SCOPE.md`
- generating architecture that conflicts with Phaser 4 + Vite + Dexie + Zod
- turning the brief into a full GDD

## Recommended structure for `docs/GAME_BRIEF.md`

The durable target brief should keep the source workflow's major sections, but
slightly compress them into a format that fits the target repo:

1. executive summary
2. game vision
3. target player and market
4. gameplay pillars and core loop
5. MVP scope and constraints
6. inspiration, competitors, and differentiators
7. world, narrative, and presentation direction
8. production risks and assumptions
9. success metrics
10. next actions and open questions

## Recommended structure for `.github/prompts/game-brief.prompt.md`

The prompt should:

1. inspect existing target docs first
2. report what is already known vs missing
3. ask only for missing brief inputs
4. produce a complete or updated `docs/GAME_BRIEF.md`
5. end with the next 1-3 follow-up actions, usually:
   - refine the brief
   - deepen `docs/ARCHITECTURE.md`
   - start the future GDD-oriented prompt flow

## Handoff rules after this conversion

Once the target repo has a stable `docs/GAME_BRIEF.md`, later conversions should
treat it as a primary input for:

- the future GDD prompt/doc flow adapted from `gds-gdd` (see
  `./spaceshipgame-gdd-conversion.md`)
- architecture deepening adapted from `gds-game-architecture`
- later scene/system/event prompts when real code begins

## What not to port

Do not carry over:

- step-file sequencing
- `_bmad` customization/runtime conventions
- frontmatter state tracking such as `stepsCompleted`
- `advanced-elicitation` and `party-mode` runtime dependencies
- installer-specific path conventions

## Recommended next conversion after this one

After the target-side game-brief prompt/doc package is implemented in
`SpaceshipGame`, the next highest-value source task is:

1. convert `gds-gdd` into a target-side GDD workflow and durable docs
