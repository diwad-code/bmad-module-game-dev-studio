# SpaceshipGame conversion workspace

This branch of [`diwad-code/bmad-module-game-dev-studio`](https://github.com/diwad-code/bmad-module-game-dev-studio) is being used as a **source repository** for adapting BMad Game Dev Studio (BMGD) ideas into the separate target project [`diwad-code/SpaceshipGame`](https://github.com/diwad-code/SpaceshipGame).

It is **not** a generic BMGD roadmap branch.

## Current goal

Use the existing BMGD agents, prompts, and workflows as source material for a **semantic conversion** into GitHub Copilot assets for `SpaceshipGame`.

The target shape is lightweight:

- `.github/prompts/`
- `.github/agents/`
- `.github/skills/`
- `docs/`
- `mechanika/`

That means we should adapt intent and knowledge, not copy BMGD runtime files 1:1.

## Approved working assumptions

- Treat `poprzednia-rozmwa.md` in the repository root as the approved branch plan.
- If a corrected `poprzednia-rozmowa.md` variant appears, treat it as the same source.
- Keep `AGENTS.md` and `docs/reference/spaceshipgame-conversion.md` aligned with that plan.
- Prefer conversion into prompts, agent docs, reusable skills, and durable project documentation.
- Do **not** port `_bmad` runtime wiring, `src/module.yaml`, `src/module-help.csv`, or `customize.toml` directly into the target repo.

## Required order of work

Before making further BMGD-side feature changes, follow this sequence:

1. Run the existing brownfield workflow against `SpaceshipGame` with `/bmgd-document-project`.
2. Generate concise durable rules with `/bmgd-generate-project-context`.
3. Review the produced documentation and `project-context.md`.
4. Only then decide whether BMGD itself needs changes to extract missing game-specific knowledge.

This branch should stay focused on improving that conversion path.

## Highest-value source areas

These BMGD areas remain the best sources for future `SpaceshipGame` conversion work:

1. `src/workflows/1-preproduction/gds-create-game-brief/`
2. `src/workflows/2-design/gds-gdd/`
3. `src/workflows/3-technical/gds-game-architecture/`
4. `src/workflows/4-production/gds-investigate/`

## Recommended next target-side conversions

1. Game brief prompt/doc flow
2. GDD workflow plus durable docs
3. Architecture prompt/doc deepening
4. Lightweight investigation prompt

## What to defer

Until `SpaceshipGame` has real code, defer:

- story implementation flows
- sprint-management flows
- test, e2e, playtest, and performance flows
- anything that assumes a runnable `src/` tree

## Source-of-truth files for this branch

- [`./poprzednia-rozmwa.md`](./poprzednia-rozmwa.md)
- [`./AGENTS.md`](./AGENTS.md)
- [`./docs/reference/spaceshipgame-conversion.md`](./docs/reference/spaceshipgame-conversion.md)
- [`./SYNC-PLAN.md`](./SYNC-PLAN.md)

## Documentation policy

README and branch-facing documentation should be updated whenever the branch goal, assumptions, workflow order, or conversion priorities change.
