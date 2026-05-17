---
title: Reference
description: Reference for the current branch mission and the underlying BMGD workflows
---

# Reference

This section now prioritizes the material needed for the current `SpaceshipGame` conversion mission.

## Branch-critical reference

- **[SpaceshipGame conversion context](./spaceshipgame-conversion.md)** — branch handoff, assumptions, and boundaries
- **[SpaceshipGame game brief conversion](./spaceshipgame-game-brief-conversion.md)** — first target-side prompt/doc conversion
- **[SpaceshipGame GDD conversion](./spaceshipgame-gdd-conversion.md)** — target-side GDD workflow and docs mapping
- **[SpaceshipGame architecture conversion](./spaceshipgame-architecture-conversion.md)** — architecture prompt/doc conversion mapping
- **[SpaceshipGame investigate conversion](./spaceshipgame-investigate-conversion.md)** — lightweight investigation prompt conversion
- **[SpaceshipGame mechanika skill conversion](./spaceshipgame-mechanika-skill-conversion.md)** — lightweight `mechanika/` helper skill mapping

## Current priority workflows

For this branch, start with these workflows before editing BMGD itself:

| Command | Purpose |
| --- | --- |
| `/bmgd-document-project` | Extract rich brownfield documentation from `SpaceshipGame` |
| `/bmgd-generate-project-context` | Turn scan output into durable implementation rules |
| `/bmgd-game-brief` | Source material for target-side game-brief conversion |
| `/bmgd-create-architecture` | Source material for target-side architecture conversion |
| `/bmgd-investigate` | Source material for a lightweight investigation prompt |

## Wider module reference

- **[Agents](./agents.md)** — BMGD's five specialized agents
- **[Workflows](./workflows.md)** — current workflow catalog
- **[Game Types](./game-types.md)** — the full set of game type templates used by the GDD flow
