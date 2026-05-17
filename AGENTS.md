# AI Work Context

This repository is `diwad-code/bmad-module-game-dev-studio`, but the current
branch work is not a normal feature change inside BMGD itself.

## Current mission on this branch

Use BMGD as the **source repository** for analyzing and selectively converting
its ideas, prompts, and workflows into the separate target repository
`diwad-code/SpaceshipGame` (sometimes described as `Spaceship-Game`).

The active branch name already reflects that goal:
`copilot/continue-repo-analysis-for-conversion`.

## What was already established

- The large BMAD-METHOD sync tracked in
  `./SYNC-PLAN.md` is finished work for BMGD v0.5.0, not the current cross-repo
  task.
- The user stated that `./poprzednia-rozmwa.md` contains the exact approved plan
  from the previous conversation. If the actual checked-in filename uses the
  corrected spelling `./poprzednia-rozmowa.md`, use that instead. Treat that
  prior-conversation file as a primary planning source for this branch when it
  is present in the checkout.
- The recent cross-repo analysis concluded that the target repo should receive
  a **semantic conversion**, not a 1:1 file port.
- BMGD uses the full module/runtime model:
  `src/module.yaml`, `src/module-help.csv`, workflow directories, `SKILL.md`,
  `customize.toml`, and `_bmad`-based conventions.
- `SpaceshipGame` currently uses a much lighter structure built around:
  `.github/prompts/`, `.github/agents/`, `.github/skills/`, `docs/`, and
  `mechanika/`.

## Verified target-repo state from the last analysis

The analysis of `diwad-code/SpaceshipGame` found:

- branch `01_github` exists and is the current integration branch for the
  target repo
- `.github/copilot-instructions.md` already defines Phaser 4, TypeScript, Vite,
  PWA-first delivery, Dexie, and Zod as the approved stack
- `.github/prompts/` already contains prompt files such as
  `game-dev.prompt.md`, `new-scene.prompt.md`, `new-system.prompt.md`,
  `new-event.prompt.md`, `data-schema.prompt.md`, `pwa-check.prompt.md`,
  `mobile-ux.prompt.md`, and `code-review.prompt.md`
- `.github/agents/` already contains lightweight planner / architect / reviewer
  agent files
- `.github/skills/` currently contains only small scaffold helpers
- `docs/` and `mechanika/` exist, but the target repo currently has **no**
  `src/` tree and **no** `package.json`

## Practical consequence

Do **not** try to port BMGD files to `SpaceshipGame` mechanically.

Prefer these mappings:

- BMGD workflow intent -> GitHub prompt file in the target repo
- BMGD agent behavior -> lightweight `.github/agents/*.agent.md`
- BMGD design guidance -> `docs/*.md` in the target repo
- small reusable scaffolds -> `.github/skills/*/SKILL.md`

Avoid directly porting runtime/module files such as:

- `src/module.yaml`
- `src/module-help.csv`
- `customize.toml`
- `_bmad`-specific wiring
- step-file orchestration that only makes sense inside the BMad runtime

## Highest-value source areas for future conversion

1. `src/workflows/1-preproduction/gds-create-game-brief/`
2. `src/workflows/2-design/gds-gdd/`
3. `src/workflows/3-technical/gds-game-architecture/`
4. `src/workflows/4-production/gds-investigate/`

## Recommended next conversions for SpaceshipGame

1. Create a dedicated game-brief prompt or doc flow from
   `gds-create-game-brief`
2. Convert `gds-gdd` into a target-side GDD workflow and durable docs
3. Reuse parts of `gds-game-architecture` to deepen
   `SpaceshipGame/docs/ARCHITECTURE.md`
4. Port `gds-investigate` into a lightweight investigation prompt

## Things to defer until the target repo has real code

Keep these for later, because `SpaceshipGame` is still mostly prompt/doc setup:

- story creation and dev-story implementation flows
- sprint management flows
- test-framework, test-design, automate, e2e, playtest, performance flows
- any conversion that assumes `src/` or a runnable app already exists

## Source-of-truth files in this repo for this branch

- `./poprzednia-rozmwa.md` (or `./poprzednia-rozmowa.md` if that is the actual
  filename) - approved action plan from the prior conversation
- `./AGENTS.md`
- `./docs/reference/spaceshipgame-conversion.md`
- `./SYNC-PLAN.md`

If another AI joins this branch, read those files first before making changes.
