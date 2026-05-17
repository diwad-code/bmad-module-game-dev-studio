---
title: "BMGD Workflows Reference"
description: Current workflow catalog with branch-specific priorities for SpaceshipGame conversion
---

# BMGD Workflows Reference

This is the current workflow catalog for BMad Game Dev Studio. On this branch, however, the **first priority** is to use the existing brownfield workflows on `SpaceshipGame` before changing BMGD itself.

## Branch priority first

Use this order for the current project:

1. `document-project`
2. `generate-project-context`
3. review the produced project docs and `project-context.md`
4. only then decide whether BMGD extraction or conversion guidance needs changes

## Anytime workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **document-project** | Technical Writer | Analyze an existing game repository and generate brownfield documentation | project knowledge docs |
| **quick-dev** | Game Solo Dev / Game Developer | Clarify, plan, implement, review, and present a requested change in one loop | implementation artifacts |
| **correct-course** | Game Architect | Recover when implementation or planning is off-track | change proposal |

## Preproduction workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **brainstorm-game** | Game Designer | Explore and refine a new game concept | brainstorming artifacts |
| **domain-research** | Game Designer | Research genre, market, and domain considerations | research notes |
| **game-brief** | Game Designer | Create a concise project brief and vision | `game-brief.md` |

## Design workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **gdd** | Game Designer | Create, update, or validate the main Game Design Document | `gdd.md` |
| **narrative** | Game Designer | Design story structure, characters, and worldbuilding | `narrative.md` |
| **create-ux-design** | Game Designer | Define UX and UI direction for player-facing flows | UX design docs |
| **prd** | Game Designer | Create, update, or validate a PRD derived from the GDD when needed | `prd.md` |

## Technical workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **generate-project-context** | Game Architect | Create durable implementation rules for future agents | `project-context.md` |
| **game-architecture** | Game Architect | Produce scale-appropriate technical architecture guidance | `architecture.md` |
| **create-epics-and-stories** | Game Architect | Break design into epics and implementation stories | epics and stories |
| **check-implementation-readiness** | Game Architect | Confirm design and architecture are aligned before production | readiness report |
| **test-framework** | Game Developer | Initialize an engine-appropriate testing foundation | test framework setup |
| **test-design** | Game Developer | Define meaningful game test scenarios | test design |

## Production workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **sprint-planning** | Game Developer | Generate or update sprint tracking from epics | `sprint-status.yaml` |
| **sprint-status** | Game Developer | Review sprint progress, risks, and next actions | status report |
| **create-story** | Game Developer | Create a story with implementation-ready context | story file |
| **dev-story** | Game Developer | Implement the story tasks and tests | completed feature |
| **code-review** | Game Developer | Perform clean-context review of completed work | review report |
| **retrospective** | Game Developer | Capture lessons after an epic or sprint | retrospective notes |
| **investigate** | Game Developer | Build an evidence-graded case file for a bug or unfamiliar subsystem | investigation case file |

## Game testing workflows

| Workflow | Agent | Purpose | Output |
| --- | --- | --- | --- |
| **test-automate** | Game Developer | Generate automated tests for the chosen engine or tooling | automated tests |
| **e2e-scaffold** | Game Developer | Scaffold end-to-end testing infrastructure | E2E scaffolding |
| **playtest-plan** | Game Developer | Create a structured playtesting plan | playtest plan |
| **performance-test** | Game Developer | Define a performance testing strategy | performance plan |
| **test-review** | Game Developer | Review test quality and coverage | test review |

## Conversion-relevant source workflows

For the current `SpaceshipGame` workstream, these are the highest-value BMGD source areas:

1. `src/workflows/1-preproduction/gds-create-game-brief/`
2. `src/workflows/2-design/gds-gdd/`
3. `src/workflows/3-technical/gds-game-architecture/`
4. `src/workflows/4-production/gds-investigate/`

## See also

- [Agents reference](./agents.md)
- [SpaceshipGame conversion context](./spaceshipgame-conversion.md)
- [SpaceshipGame game brief conversion](./spaceshipgame-game-brief-conversion.md)
- [SpaceshipGame GDD conversion](./spaceshipgame-gdd-conversion.md)
