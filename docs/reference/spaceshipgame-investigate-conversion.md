---
title: "SpaceshipGame Investigate Conversion"
description: How to adapt BMGD's investigation workflow into a lightweight Copilot prompt for SpaceshipGame
---

# SpaceshipGame investigate conversion

This note defines the fourth concrete source-to-target conversion for the
current branch: adapting `gds-investigate` into a lightweight GitHub Copilot
investigation flow for `diwad-code/SpaceshipGame`.

## Why this conversion should stay minimal

`gds-investigate` is valuable because it enforces evidence-first investigation
instead of guess-driven debugging.

However, `SpaceshipGame` is still earlier than a typical production repository:

- the prompt and docs layer is already substantial
- the code layer is still limited or emerging
- `mechanika/` is still expected to define major gameplay rules later

Because of that, the target repo should not receive the full BMad case-file
workflow yet. It should receive only a minimal investigation prompt that helps
the user inspect repo state, prompt/doc conflicts, setup failures, and later
implementation bugs when real code exists.

## Source workflow shape in BMGD

The source workflow lives in:

- `src/workflows/4-production/gds-investigate/SKILL.md`
- `src/workflows/4-production/gds-investigate/references/case-file-template.md`

Its durable value is not the runtime orchestration. The value is:

- evidence grading: confirmed, deduced, hypothesized
- stronghold-first investigation
- explicit missing-evidence tracking
- a clean hand-off summary for the next engineer
- disciplined stopping at diagnosis rather than speculative implementation

## Source workflow behaviors worth preserving

The most valuable source behaviors to carry over are:

1. inspect evidence before proposing theories
2. separate confirmed findings from hypotheses
3. challenge the initial problem statement when evidence contradicts it
4. surface missing evidence explicitly
5. end with a concrete next action instead of an open-ended narrative

## Target-side artifact set for SpaceshipGame

Do not port the runtime mechanics. Convert the workflow into these lightweight
target artifacts:

| Target artifact | Purpose | Priority |
| --- | --- | --- |
| `.github/prompts/investigate.prompt.md` | interactive Copilot prompt for repo-state, setup, prompt, doc, and later code investigations | High |
| `docs/COPILOT_WORKFLOW.md` update | explain when to use the investigation prompt instead of `game-dev` or `code-review` | High |
| `docs/INVESTIGATIONS/` optional later | durable investigation notes only when the target repo has enough code/debug history to justify them | Low |

Optional later additions:

- `.github/agents/game-reviewer.agent.md` update if the target repo later wants
  the reviewer to route deep debugging requests toward the investigation prompt
- a reusable issue template only if the target repo starts accumulating bug
  reports and reproducible regressions

## Recommended target behavior

The target repo should not recreate BMGD's persistent case files, step-by-step
checkpointing, or large evidence inventories by default.

Instead:

- use one prompt file as the entry point
- start from the user's concrete symptom, file, error, or repo area
- inspect actual workspace files before theorizing
- classify findings as confirmed, deduced, or hypothesized
- stop at diagnosis and recommended next action unless the user explicitly asks
  for implementation

## Source-to-target mapping

| BMGD source element | SpaceshipGame destination | Adaptation note |
| --- | --- | --- |
| `SKILL.md` evidence-first investigation flow | `.github/prompts/investigate.prompt.md` | compress the full workflow into one prompt that supports investigate, explain, and diagnose modes |
| `case-file-template.md` | structured prompt output block | preserve sections like findings, hypotheses, missing evidence, and next steps, but keep them in response text first |
| case-file persistence | optional `docs/INVESTIGATIONS/*.md` later | do not require durable case files until the target repo actually benefits from them |
| stronghold-first evidence discipline | prompt instructions | require Copilot to anchor on one confirmed fact before expanding scope |
| outcome routing to other workflows | prompt closing actions | recommend `game-dev`, `code-review`, or implementation prompts based on what the investigation finds |

## SpaceshipGame-specific adjustments

The target conversion must absorb the target repo's current rules:

- use existing project authority order from `docs/ARCHITECTURE.md`
- respect `docs/SCOPE.md` for MVP boundaries
- treat `mechanika/` as authoritative for finalized gameplay rules
- keep Phaser 4, TypeScript, Vite, Dexie, and Zod as fixed architecture choices
  unless an ADR changes them

Because of that, the converted investigation prompt should explicitly prevent
Copilot from:

- inventing missing mechanics just to explain a bug
- proposing architecture rewrites before checking the accepted docs
- treating Claude notes or speculative ideas as evidence
- drifting from diagnosis into uncontrolled implementation

## Recommended use cases in the target repo

At the current maturity level of `SpaceshipGame`, the minimal investigation
prompt should focus on:

1. project-state contradictions between prompts, docs, and repo files
2. setup failures after the first Vite/Phaser scaffolding lands
3. architecture mismatches, such as business logic leaking into scenes
4. data-shape, save, PWA, and mobile regressions once code exists
5. ambiguity about whether a request is blocked by `mechanika/`

It should be lower priority for:

- broad gameplay design exploration already covered by the brief or GDD prompts
- code review tasks already covered by `code-review.prompt.md`
- normal project orchestration already covered by `game-dev.prompt.md`

## Recommended structure for `.github/prompts/investigate.prompt.md`

The prompt should:

1. inspect:
   - `.github/copilot-instructions.md`
   - relevant `docs/`
   - `mechanika/`
   - relevant prompt, agent, or code files mentioned by the user
2. restate the reported issue as a hypothesis, not a fact
3. identify one confirmed stronghold before expanding the search
4. return findings under clear sections such as:
   - confirmed findings
   - deduced conclusions
   - open hypotheses
   - missing evidence
   - recommended next action
5. recommend the next prompt or implementation step only after the diagnosis is
   clear

## Validation expectations for the target prompt

The target prompt should preserve the spirit of `gds-investigate` by ensuring:

- the response cites real repo evidence
- hypotheses are clearly labeled as unconfirmed
- contradictions to the user's premise are stated directly
- missing evidence is called out explicitly
- the prompt does not silently switch from diagnosis to coding

## What not to port

Do not carry over:

- `_bmad` runtime and customization wiring
- mandatory case-file creation for every investigation
- large process-state templates when a short prompt response is enough
- workflow outcome numbering and micro-step orchestration
- production-scale forensic overhead before the target repo has matching scale

## Recommended next step after this conversion

After this source-to-target handoff is documented, the highest-value next action
is no longer another conversion spec inside BMGD. The next useful work is:

1. implement the converted prompt/doc artifacts in `SpaceshipGame`, or
2. return to the approved branch plan and evaluate real target-repo scan results
   before changing BMGD workflows further
