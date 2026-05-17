---
title: "SpaceshipGame Mechanika Skill Conversion"
description: How to add a lightweight Copilot skill for authoring and refining gameplay specs in mechanika/
---

# SpaceshipGame mechanika skill conversion

This note defines the third concrete source-to-target conversion for the current
branch: adding a small Copilot skill that helps `diwad-code/SpaceshipGame`
author and refine individual gameplay-spec files in `mechanika/`.

## Why this conversion comes third

This skill should be implemented only after the target repo has:

1. `.github/prompts/game-brief.prompt.md` and `docs/GAME_BRIEF.md`
2. `.github/prompts/gdd.prompt.md`, `docs/GDD.md`, and `docs/EPICS.md`

That order matters because the skill is not supposed to invent game direction on
its own. It should reuse the stable brief and GDD context so Copilot can expand
or refine mechanics without drifting away from the agreed product vision.

## What problem this skill solves

`SpaceshipGame` already has a `mechanika/` area, but a generic prompt is not the
best tool for editing one focused gameplay spec at a time.

The lightweight skill should help Copilot:

- create a missing mechanic spec from the current brief/GDD context
- refine one existing mechanic file without rewriting unrelated design areas
- separate confirmed rules from placeholders, assumptions, and open questions
- keep `mechanika/` aligned with `docs/GAME_BRIEF.md`, `docs/GDD.md`, and
  `docs/SCOPE.md`

## Source value to preserve from BMGD

Do not port a full BMad runtime workflow. Preserve only the durable behaviors
that matter for mechanic-spec authoring:

- evidence-first use of existing project context
- explicit scope boundaries before adding detail
- structured outputs instead of free-form brainstorming
- clear handoff to the next design or implementation step

## Target-side artifact set for SpaceshipGame

Convert the source intent into these lightweight target artifacts:

| Target artifact | Purpose | Priority |
| --- | --- | --- |
| `.github/skills/mechanika-spec/SKILL.md` | focused helper for creating or updating one mechanic spec in `mechanika/` | High |
| `.github/skills/mechanika-spec/examples/` optional later | tiny examples only if the target repo needs repeatable spec shapes | Low |
| `docs/COPILOT_WORKFLOW.md` update | explain that the skill is used after the brief and GDD exist | High |

## Recommended target behavior

The skill should stay narrow and tactical.

It should:

1. inspect the existing brief, GDD, scope, and relevant files in `mechanika/`
2. identify what is already settled versus still missing
3. work on one mechanic or one tightly related mechanic cluster at a time
4. update or create a single durable spec file in `mechanika/`
5. finish with open questions, dependencies, and the next recommended follow-up

It should not:

- act like a full GDD workflow
- redefine product vision already captured in `docs/GAME_BRIEF.md`
- replace `docs/GDD.md` as the design source of truth
- speculate about implementation architecture that belongs in
  `docs/ARCHITECTURE.md`

## Scope of the skill

The skill should be good at guiding Copilot through spec work such as:

- core loop refinements
- economy or resource rules
- event logic and consequences
- progression pacing
- narrative hooks attached to mechanics
- dependencies between mechanics
- unresolved questions and deferred details

## Recommended structure for `.github/skills/mechanika-spec/SKILL.md`

The skill should instruct Copilot to:

1. inspect:
   - `.github/copilot-instructions.md`
   - `docs/GAME_BRIEF.md`
   - `docs/GDD.md`
   - `docs/EPICS.md` if present
   - `docs/SCOPE.md`
   - the relevant files under `mechanika/`
2. restate the requested mechanic and its design purpose
3. distinguish:
   - confirmed rules
   - inferred constraints
   - unresolved mechanics
   - dependencies on other `mechanika/` files
4. create or update the target mechanic spec with concise sections such as:
   - purpose
   - player-facing behavior
   - rules and constraints
   - dependencies
   - edge cases
   - open questions
5. end with the next 1-3 follow-up actions, usually:
   - refine a related mechanic spec
   - update `docs/GDD.md` if the mechanic changed the design contract
   - update `docs/ARCHITECTURE.md` only if the mechanic creates a new technical boundary

## Relationship to other target-side conversions

Use this sequence:

1. game brief conversion first
2. GDD conversion second
3. mechanika skill third
4. architecture conversion after the design layer is stable
5. investigation conversion later, once the target repo needs diagnosis flows

## What not to port

Do not carry over:

- `_bmad` runtime conventions
- multi-step workflow state tracking
- generic installer/customization wiring
- broad story/sprint flows that assume a runnable codebase
- any skill behavior that edits many unrelated design files in one pass

## Recommended next conversion after this one

After the target-side mechanika skill is implemented in `SpaceshipGame`, the
next highest-value source task is:

1. use `./spaceshipgame-architecture-conversion.md` to implement the
   target-side architecture prompt/doc package adapted from
   `gds-game-architecture`
