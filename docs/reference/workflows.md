---
title: "BMGD Workflows Reference"
description: Complete catalog of all BMad Game Dev Studio workflows
---

# BMGD Workflows Reference

Complete catalog of all BMad Game Dev Studio workflows organized by development phase and purpose.

---

## Quick Flow Workflows

Rapid prototyping workflows for solo developers and small teams.

| Workflow | Agent | Purpose | Prerequisites |
|----------|-------|---------|--------------|
| **quick-prototype** | Indie | Create a rapid game prototype for early validation | Game engine installed |
| **quick-dev** | Indie | Quick development iteration with game-specific guidance | Existing prototype |
| **quick-spec** | Indie | Generate a quick game specification | Game concept |

**Use when:** You want to test ideas fast, work alone, or need a playable prototype quickly.

---

## Preproduction Workflows

Define your game concept and vision before committing to production.

| Workflow | Agent | Purpose | Outputs |
|----------|-------|---------|---------|
| **brainstorm-game** | Game Designer | Generate game ideas using specialized techniques | Game concept |
| **game-brief** | Game Designer | Create a project brief capturing vision and positioning | `game-brief.md` |

**Use when:** You're starting a new project and need to define what you're building.

---

## Design Workflows

Create comprehensive game design documentation.

| Workflow | Agent | Purpose | Outputs |
|----------|-------|---------|---------|
| **create-gdd** | Game Designer | Create a Game Design Document with 24 game type templates | `gdd.md` |
| **narrative** | Game Designer | Design narrative elements and story | `narrative.md` |

**Use when:** You have a game concept and need to document the design.

**Game Type Templates Available:** Action Platformer, Adventure, Card Game, Fighting, Horror, Idle/Incremental, Metroidvania, MOBA, Party Game, Puzzle, Racing, Rhythm, Roguelike, RPG, Sandbox, Shooter, Simulation, Sports, Survival, Strategy, Text-Based, Tower Defense, Turn-Based Tactics, Visual Novel

---

## Technical Workflows

Plan your technical architecture and project structure.

| Workflow | Agent | Purpose | Outputs |
|----------|-------|---------|---------|
| **document-project** | Technical Writer | Analyze an existing game repository and generate brownfield documentation | Project knowledge docs |
| **create-architecture** | Game Architect | Create game architecture with engine-specific patterns | `architecture.md` |
| **generate-project-context** | Game Architect | Create project context for AI consistency | `project-context.md` |
| **correct-course** | Game Architect | Course correction when implementation is off-track | Analysis report |

**Use when:** You need to understand an existing game project, plan how to build your game, or get implementation back on track.

---

## Production Workflows

Plan and track development through sprints and stories.

| Workflow | Agent | Purpose | Outputs |
|----------|-------|---------|---------|
| **sprint-planning** | Game Scrum Master | Generate sprint status from epic files | `sprint-status.yaml` |
| **sprint-status** | Game Scrum Master | View sprint progress, risks, and next actions | Status report |
| **create-story** | Game Scrum Master | Create story with ready-for-dev marking | Story file in `stories/` |
| **dev-story** | Game Developer | Implement story tasks with tests | Completed feature |
| **code-review** | Game Developer | Perform clean context QA code review | Review report |
| **retrospective** | Game Scrum Master | Facilitate retrospective after epic completion | Retrospective notes |

**Use when:** You're ready to build features, track progress, or review work.

---

## Testing Workflows

Set up and run game testing across all phases.

| Workflow | Agent | Purpose | Outputs |
|----------|-------|---------|---------|
| **test-framework** | Game QA | Initialize game test framework (Unity/Unreal/Godot) | Test project setup |
| **test-design** | Game QA | Create comprehensive game test scenarios | Test plan |
| **automate** | Game QA | Generate automated game tests | Test suite |
| **e2e-scaffold** | Game QA | Scaffold E2E testing infrastructure | E2E test framework |
| **playtest-plan** | Game QA | Create structured playtesting plan | Playtest plan |
| **performance** | Game QA | Design performance testing strategy | Performance test plan |
| **test-review** | Game QA | Review test quality and coverage | Coverage report |

**Use when:** You need to test your game, set up automation, or plan playtesting.

---

## Workflow Reference by Agent

### Game Designer (Samus Shepard)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| brainstorm-game | Preproduction | Generate and refine game ideas |
| game-brief | Preproduction | Create project brief |
| create-gdd | Design | Create Game Design Document |
| narrative | Design | Design story and narrative |

### Game Architect (Cloud Dragonborn)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| create-architecture | Technical | Create technical architecture |
| generate-project-context | Technical | Create project context |
| correct-course | Production | Course correction analysis |

### Technical Writer (Paige)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| document-project | Technical | Document an existing game repository for AI-assisted development |

### Game Developer (Link Freeman)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| dev-story | Production | Implement story tasks |
| code-review | Production | Review code quality |
| quick-dev | Quick Flow | Quick development iteration |

### Game Scrum Master (Max)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| sprint-planning | Production | Plan sprints from epics |
| sprint-status | Production | View sprint progress |
| create-story | Production | Create implementation stories |
| retrospective | Production | Facilitate retrospective |

### Game QA (GLaDOS)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| test-framework | Any | Initialize test framework |
| test-design | Any | Create test scenarios |
| automate | Any | Generate automated tests |
| e2e-scaffold | Any | Scaffold E2E testing |
| playtest-plan | Any | Plan playtesting sessions |
| performance | Any | Performance testing strategy |
| test-review | Any | Review test coverage |

### Game Solo Dev (Indie)

| Workflow | Phase | Purpose |
|----------|-------|---------|
| quick-prototype | Quick Flow | Create rapid prototype |
| quick-dev | Quick Flow | Quick development |
| quick-spec | Quick Flow | Quick specification |

---

## See Also

- **[Agents Reference](./agents.md)** — Learn about all 5 BMGD agents
- **[Quick Flow vs Full Production](../explanation/quick-flow-vs-full.md)** — Choose your development approach
- **[Game Types Reference](./game-types.md)** — All 24 game type templates
