---
title: "SpaceshipGame Conversion Context"
description: Current cross-repo analysis for adapting BMGD content into SpaceshipGame
---

# SpaceshipGame conversion context

This note captures the current branch-level objective for AI collaborators.

The repository under edit is `diwad-code/bmad-module-game-dev-studio`, but the current task is to use BMGD as the **analysis source** for work that will later be applied to the separate target repository `diwad-code/SpaceshipGame`.

## Why this document exists

The previous session established conversion rules and target-repo findings in chat, but that context was not stored in tracked files.

This file turns that session state into repo-visible context so future agents do not need to reconstruct it from memory.

The user later clarified that a root-level prior-conversation markdown file contains the exact approved action plan from the earlier conversation. Future AI sessions should read `./poprzednia-rozmwa.md` first, because that is the filename used in the user comment, and treat that prior-conversation file as the most specific branch-level plan when it is available in the checkout. If a corrected `./poprzednia-rozmowa.md` variant appears instead, treat it as the same handoff source. If neither file is present, use this document and `./AGENTS.md` as the fallback handoff context.

## Current target-repo understanding

The analyzed target repository is public at <https://github.com/diwad-code/SpaceshipGame>.

The last verified findings were:

- default working branch for the target analysis: `01_github`
- target repo is still in a pre-code or Sprint 0 state
- target repo already has structured Copilot assets under `.github/`
- target repo already has project docs under `docs/`
- target repo already has mechanics placeholders and spec files under `mechanika/`
- target repo does **not** yet have `src/`
- target repo does **not** yet have `package.json`

## Core conversion decision

The conversion target is **not** another BMGD module.

That means this work must be a **semantic adaptation** of BMGD knowledge into a GitHub prompt, doc, and agent layout, rather than a file-for-file transplant.

## Current required workflow order

Before making further BMGD-side feature changes, use the module on the real target repo first:

1. run `/bmgd-document-project` (`gds-document-project`) on `SpaceshipGame`
2. prefer a deep or exhaustive scan
3. run `/bmgd-generate-project-context` (`gds-generate-project-context`)
4. inspect the produced docs and `project-context.md`
5. only then decide whether BMGD itself needs changes

This is the shortest path to discovering real extraction gaps instead of guessing them from summaries.

## Source vs target model

| BMGD source model | SpaceshipGame target model |
| --- | --- |
| `src/module.yaml` roster and module config | lightweight `.github/agents/*.agent.md` plus docs |
| `src/module-help.csv` catalog | human-readable docs and prompt names |
| workflow `SKILL.md` plus `customize.toml` | `.github/prompts/*.prompt.md` or small skills |
| `_bmad` config and runtime wiring | plain repo docs and prompt instructions |
| step-file orchestration | concise prompt workflows |

## Recommended mapping by area

| BMGD source area | Target-side destination | Priority | Notes |
| --- | --- | --- | --- |
| `gds-create-game-brief` | new prompt and doc flow for game briefing | High | best first concrete conversion |
| `gds-gdd` | GDD prompt plus durable `docs/` artifacts | High | strongest design asset to carry over |
| `gds-game-architecture` | deeper architecture guidance in `docs/ARCHITECTURE.md` and prompts | High | reuse content, not runtime structure |
| `gds-investigate` | lightweight investigation prompt | Medium | especially useful once the target repo becomes more complex |
| `gds-create-story` and `gds-dev-story` | defer | Low | target repo has no implementation tree yet |
| sprint and testing flows | defer | Low | too early before runnable code exists |

## Recommended implementation order

If the immediate goal is to help Copilot produce durable design content in `SpaceshipGame/mechanika/`, use this order:

1. implement the game-brief prompt and doc package
2. implement the GDD prompt and doc package
3. implement the lightweight `mechanika/` helper skill
4. deepen architecture guidance
5. add a minimal investigation prompt

## Things that should not be ported directly

Do not directly convert these into the target repo:

- `src/module.yaml`
- `src/module-help.csv`
- `customize.toml`
- `_bmad` path conventions
- skill activation sequences that depend on BMad runtime scripts
- engine-agnostic bulk content that ignores the target repo's approved Phaser 4 stack

## Documentation policy for this branch

Keep this file, the docs entry points, and the root README updated whenever the approved plan, target assumptions, or conversion order changes.
