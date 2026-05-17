---
title: "Analyze an existing game project with BMGD"
description: Use BMGD to document a brownfield game repository and generate durable AI context
---

# Analyze an existing game project with BMGD

Use this workflow when you already have a playable or in-progress game repository and want BMGD to extract project knowledge before making changes.

For the current branch, this guide is the **required first step** before proposing more BMGD-side conversion changes for `SpaceshipGame`.

## When to use this guide

- you have an existing Unity, Unreal, Godot, Phaser, or custom-engine repository
- you want Copilot or other agents to understand the codebase before implementation
- you need brownfield documentation, architecture notes, and developer commands
- you want a `project-context.md` file that captures durable implementation rules

## Before you start

Make sure the repository is accessible from your BMad-enabled environment:

- the project is cloned locally **or** the public repository link is reachable
- you can open the project root in the same workspace where BMGD runs
- you have permission to analyze the code and keep local documentation artifacts

For this branch, the target repository is `diwad-code/SpaceshipGame`.

## Required workflow order

### Step 1: Document the existing project

Start with the brownfield documentation workflow:

```text
/bmgd-document-project
```

This invokes the **Technical Writer (Paige)** to analyze the repository and generate project knowledge such as:

- repository structure
- technology stack and versions
- architecture patterns
- key features and integration points
- developer commands and setup notes
- existing documentation inventory

### Step 2: Choose a deep enough scan

When prompted for scan depth, prefer:

- **Deep Scan** for most active game projects
- **Exhaustive Scan** when you want the richest possible AI context

Avoid Quick Scan unless you only need a lightweight overview. For brownfield implementation and conversion work, deeper scans produce better context for later agent tasks.

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

```text
/bmgd-generate-project-context
```

This invokes the **Game Architect (Cloud Dragonborn)** to create `project-context.md`, a concise guide containing:

- engine and tooling decisions
- naming and organization conventions
- performance-sensitive rules
- testing expectations
- implementation constraints that agents should not miss

### Step 5: Decide whether BMGD needs changes

Only after reviewing the documentation output and `project-context.md` should you decide whether the module itself needs better extraction rules.

Examples of valid reasons to change BMGD after the scan:

- the documentation workflow misses game-mechanic structure that matters later
- the generated context ignores important repo conventions
- the scan under-describes assets, project organization, or design documents

## Suggested next steps

- use the SpaceshipGame conversion reference docs to plan target-side prompt and doc adaptations
- if important game-specific details are missing, improve the extraction guidance in BMGD based on those observed gaps
- update `project-context.md`, this guide, and the root README whenever the branch workflow changes

## Related guides

- [How-to overview](./index.md)
- [SpaceshipGame conversion context](../reference/spaceshipgame-conversion.md)
- [Workflows reference](../reference/workflows.md)
