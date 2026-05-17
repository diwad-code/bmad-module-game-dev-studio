---
title: "SpaceshipGame Conversion Context"
description: Current cross-repo analysis for adapting BMGD content into SpaceshipGame
---

# SpaceshipGame conversion context

This note captures the current branch-level objective for AI collaborators.

The repository under edit is `diwad-code/bmad-module-game-dev-studio`, but the
current task is to use BMGD as the **analysis source** for work that will later
be applied to the separate target repository `diwad-code/SpaceshipGame`.

## Why this document exists

The previous session established conversion rules and target-repo findings in
chat, but that context was not stored in tracked files.

This file turns that session state into repo-visible context so future agents do
not need to reconstruct it from memory.

The user later clarified that a root-level prior-conversation markdown file
contains the exact approved action plan from the earlier conversation. Future
AI sessions should read `./poprzednia-rozmwa.md` first, because that is the
filename used in the user comment, and treat that prior-conversation file as
the most specific branch-level plan when it is available in the checkout. If a
corrected `./poprzednia-rozmowa.md` variant appears instead, treat it as the
same handoff source. If neither file is present, use this document and
`./AGENTS.md` as the fallback handoff context.

## Current target-repo understanding

The analyzed target repository is public at
<https://github.com/diwad-code/SpaceshipGame>.

The last verified findings were:

- default working branch for the target analysis: `01_github`
- target repo is still in a pre-code / Sprint 0 state
- target repo already has structured Copilot assets under `.github/`
- target repo already has project docs under `docs/`
- target repo already has mechanics placeholders/spec files under `mechanika/`
- target repo does **not** yet have `src/`
- target repo does **not** yet have `package.json`

## What already exists in SpaceshipGame

### Prompt layer

The target repo already contains prompt files for:

- project orchestration
- new scenes
- new systems
- new events
- data schemas
- PWA checks
- mobile UX review
- code review

### Agent layer

The target repo already contains lightweight agent files for:

- planner
- architect
- reviewer

### Rules layer

The target repo already has durable rules in:

- `.github/copilot-instructions.md`
- `docs/ARCHITECTURE.md`
- `docs/SCOPE.md`
- `docs/IDEAS_LATER.md`
- `docs/COPILOT_WORKFLOW.md`
- `mechanika/`

## Core conversion decision

The conversion target is **not** another BMGD module.

That means this work must be a **semantic adaptation** of BMGD knowledge into a
GitHub prompt/doc/agent layout, rather than a file-for-file transplant.

## Source vs target model

| BMGD source model | SpaceshipGame target model |
| --- | --- |
| `src/module.yaml` roster and module config | lightweight `.github/agents/*.agent.md` plus docs |
| `src/module-help.csv` catalog | human-readable docs and prompt names |
| workflow `SKILL.md` + `customize.toml` | `.github/prompts/*.prompt.md` or small skills |
| `_bmad` config/runtime wiring | plain repo docs and prompt instructions |
| step-file orchestration | concise prompt workflows |

## Recommended mapping by area

| BMGD source area | Target-side destination | Priority | Notes |
| --- | --- | --- | --- |
| `gds-create-game-brief` | new prompt/doc flow for game briefing | High | Best next discovery artifact |
| `gds-gdd` | GDD prompt + durable `docs/` artifacts | High | Strongest design asset to carry over |
| `gds-game-architecture` | deeper architecture guidance in `docs/ARCHITECTURE.md` and prompts | High | Reuse only content, not runtime structure |
| `gds-investigate` | lightweight investigation prompt | Medium | Useful once the target repo has code or complex docs |
| `gds-create-story` / `gds-dev-story` | defer | Low | Target repo has no implementation tree yet |
| test and sprint workflows | defer | Low | Too early before runnable code exists |

## Things that should not be ported directly

Do not directly convert these into the target repo:

- `src/module.yaml`
- `src/module-help.csv`
- `customize.toml`
- `_bmad` path conventions
- skill activation sequences that depend on BMad runtime scripts
- engine-agnostic bulk content that ignores the target repo's approved Phaser 4
  stack

## Current branch intent

When editing this branch, prefer changes that help with:

1. preserving the cross-repo context
2. making the current conversion goal legible to future AIs
3. identifying which BMGD materials are worth adapting next
4. staying aligned with the approved plan recorded in the prior-conversation
   file (`./poprzednia-rozmwa.md`, or the corrected
   `./poprzednia-rozmowa.md` variant if that is what exists)

Do not treat this branch as a general BMGD roadmap branch unless the user says
otherwise.

## Open issues

- The GitHub task URL referenced by the user was not retrievable from this
  environment during this session, so its exact text is not preserved here.
- No tracked file in this repo previously captured the SpaceshipGame conversion
  context, which is why this note was added.
- During the PR comment follow-up, the user referenced a root-level
  prior-conversation markdown file as the approved plan, but it was not visible
  in this local checkout. If a later fetch or commit adds
  `./poprzednia-rozmwa.md`, or the corrected `./poprzednia-rozmowa.md`
  variant, that file should take precedence over this summary where they
  differ.

## Suggested next action for the next AI

Pick one of these and continue:

1. use `./docs/reference/spaceshipgame-game-brief-conversion.md` as the source
   spec for implementing the target-side game-brief prompt/doc package in
   `SpaceshipGame`
2. use `./docs/reference/spaceshipgame-gdd-conversion.md` as the source spec
   for implementing the target-side GDD prompt/doc package in `SpaceshipGame`
3. use `./docs/reference/spaceshipgame-architecture-conversion.md` as the
   source spec for implementing the target-side architecture prompt/doc package
   in `SpaceshipGame`
4. use `./docs/reference/spaceshipgame-investigate-conversion.md` as the source
   spec for implementing a minimal target-side investigation prompt
