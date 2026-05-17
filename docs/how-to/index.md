---
title: "How-To Guides"
description: Practical guidance for the current SpaceshipGame conversion workflow
---

# How-To Guides

For this branch, the practical workflow is centered on **brownfield analysis first** and only then on BMGD-side adjustments.

## Primary workflow for the current project

1. **[Analyze an existing game project with BMGD](./analyze-existing-game-project.md)**
   - run the documentation workflow on `SpaceshipGame`
   - prefer deep or exhaustive scanning
   - capture structure, architecture, commands, and conventions
2. **Generate `project-context.md`**
   - use `/bmgd-generate-project-context` after the scan
   - turn the scan output into short durable rules for later agents
3. **Evaluate gaps**
   - compare the generated output with the real needs of `SpaceshipGame`
   - only then decide whether BMGD extraction guidance must change
4. **Use the reference conversion specs**
   - game brief
   - GDD
   - architecture
   - investigation

## Secondary BMGD guides still available

These remain useful when you need background on the wider module:

- [Set up a Unity project with BMGD](./setup-unity.md)
- [Set up an Unreal project with BMGD](./setup-unreal.md)
- [Set up a Godot project with BMGD](./setup-godot.md)
- [Run sprint planning with BMGD](./sprint-planning.md)

## Reference links

- [Workflows reference](../reference/workflows.md)
- [Agents reference](../reference/agents.md)
- [SpaceshipGame conversion context](../reference/spaceshipgame-conversion.md)
