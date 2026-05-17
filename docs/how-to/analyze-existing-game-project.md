---
title: "Analyze an existing game project with BMGD"
description: Use BMGD to document a brownfield game repository and generate durable AI context
---

# Analyze an existing game project with BMGD

Use this workflow when you already have a playable or in-progress game repository and want BMGD to extract project knowledge before making changes.

---

## When to Use This Guide

- You have an existing Unity, Unreal, Godot, or custom-engine game repository
- You want Copilot or other agents to understand the codebase before implementation
- You need brownfield documentation, architecture notes, and developer commands
- You want a `project-context.md` file that captures durable implementation rules

---

## Before You Start

Make sure the repository is accessible from your BMad-enabled environment:

- The project is cloned locally **or** the public repository link is reachable
- You can open the project root in the same workspace where BMGD runs
- You have permission to analyze the code and keep local documentation artifacts

---

## Recommended Workflow

### Step 1: Document the existing project

Start with the brownfield documentation workflow:

```
/bmgd-document-project
```

This invokes the **Technical Writer (Paige)** to analyze the repository and generate project knowledge such as:

- Repository structure
- Technology stack and versions
- Architecture patterns
- Key features and integration points
- Developer commands and setup notes
- Existing documentation inventory

### Step 2: Choose a deep enough scan

When prompted for scan depth, prefer:

- **Deep Scan** for most active game projects
- **Exhaustive Scan** when you want the richest possible AI context

Avoid Quick Scan unless you only need a lightweight overview. For brownfield implementation work, deeper scans produce better context for later agent tasks.

### Step 3: Review the generated documentation

After the scan completes, review the generated files in the workflow output folder, especially:

- `index.md`
- `project-overview.md`
- `architecture.md`
- `development-guide.md`
- `source-tree-analysis.md`

These documents should give you a working picture of the repository before any implementation begins.

### Step 4: Generate project context for agents

Once the documentation looks solid, create the rules file that other agents will rely on:

```
/bmgd-generate-project-context
```

This invokes the **Game Architect (Cloud Dragonborn)** to create `project-context.md`, a concise guide containing:

- Engine and tooling decisions
- Naming and organization conventions
- Performance-sensitive rules
- Testing expectations
- Implementation constraints that agents should not miss

### Step 5: Use `project-context.md` as the source of truth

After both workflows complete, treat `project-context.md` as the durable implementation guide for future BMGD and Copilot tasks.

This is the best path when you want to:

- onboard a coding agent to an unfamiliar game project
- reduce repeated codebase rediscovery
- keep future implementation consistent with the existing repository

---

## Suggested Next Steps

- Run implementation workflows such as `/bmgd-dev-story` only after the repository has been documented
- If important game-specific details are still missing, rerun `document-project` with a deeper scan or use deep-dive mode on the subsystem you care about
- Update `project-context.md` whenever major architecture or pipeline decisions change

---

## Related Guides

- [Set up a Unity project with BMGD](./setup-unity.md)
- [Set up an Unreal project with BMGD](./setup-unreal.md)
- [Set up a Godot project with BMGD](./setup-godot.md)
- [Workflows Reference](../reference/workflows.md)
