# How To Use The Codex Development Studio

This studio is useful only when each role leaves visible evidence of its work.
Do not treat the agent files as decoration. Treat them as an operating process:

1. Discuss the goal.
2. Run one tier at a time.
3. Save each tier's run log.
4. Save each tier's deliverable.
5. Get approval before handing off to the next tier.

## Core Idea

The coordinator is not the whole studio.

The user is also not the project manager. The coordinator must follow
`orchestrator.md` to decide the next stage automatically whenever the user says
`/start`, `next`, or `Continue the studio workflow`.

The coordinator should:

- read the user's request
- read existing studio artifacts
- choose the correct workflow
- call the right role at the right time
- keep the project moving
- review and merge outputs
- make every role's work auditable

Each role should:

- receive a clear input
- produce one concrete artifact
- record decisions, non-goals, risks, and handoff notes

## Folder Map

- `agents/`: role definitions and responsibility boundaries
- `workflows/`: ordered procedures for common project work
- `rules/`: quality gates and domain constraints
- `session-state/active.md`: current project memory
- `orchestrator.md`: automatic stage detection and handoff rules
- `studio-runs/`: recommended folder for visible role run logs

If `studio-runs/` does not exist in the target project, create it under that
project's `docs/` folder.

## The Required Run Log

Every tier should create a run log before the next tier starts.

Recommended path:

```text
docs/studio-runs/YYYY-MM-DD-tier-N-role-name.md
```

The run log should include:

- date
- tier
- role
- input received
- work performed
- decisions made
- rejected scope / non-goals
- output artifact
- handoff recommendation
- approval status

Without this file, the studio is not auditable.

## Standard Tier Flow

The coordinator should not require the user to remember this flow. This section
explains the process; `orchestrator.md` is the rulebook the coordinator follows.

### Tier 1: Product

Role:

- `product-lead`

Purpose:

- turn discussion into product scope
- define V1, non-goals, acceptance criteria, and risks

Artifacts:

- `docs/product-lead-brief.md`
- `docs/studio-runs/YYYY-MM-DD-tier-1-product-lead.md`

Approval question:

```text
Do you approve this product scope, or should we change it before UX/Data/Frontend?
```

Do not start implementation before Tier 1 is approved.

### Tier 2: Planning

Roles:

- `ux-designer`
- `data-api-engineer`
- `seo-content-specialist`

Purpose:

- translate approved product scope into page flow, data model, and SEO/content
  structure

Artifacts:

- `docs/ux-designer-brief.md`
- `docs/data-api-brief.md`
- `docs/seo-content-brief.md`
- one run log for each role

These roles may run in parallel if their inputs are clear.

Approval question:

```text
Do you approve these implementation briefs?
```

Do not start frontend implementation before Tier 2 is approved.

### Product Gate: Tier 2 Review

Role:

- `product-lead`

Purpose:

- review Tier 2 decisions before implementation
- catch scope creep
- approve or block Tier 3

Artifacts:

- `docs/product-lead-review.md`
- `docs/studio-runs/YYYY-MM-DD-product-lead-tier-2-review.md`

This gate is mandatory. The user should not need to ask for it.

### Tier 3: Implementation

Roles:

- `frontend-engineer`
- optionally `data-api-engineer` if data code changes are needed

Purpose:

- implement the approved pages, data contracts, and UI behavior

Artifacts:

- code changes
- `docs/studio-runs/YYYY-MM-DD-tier-3-frontend-engineer.md`

Implementation roles must list changed files in the run log.

### Tier 4: Verification

Roles:

- `qa-tester`
- `performance-reviewer`

Purpose:

- test behavior, responsiveness, layout stability, data states, and performance
  risks

Artifacts:

- `docs/qa-report.md`
- `docs/performance-review.md`
- one run log for each role

Approval question:

```text
Do we ship, revise, or defer?
```

## How To Ask Codex To Use The Studio

Use explicit language so Codex knows you want visible staged studio work.

Best starting prompt:

```text
/start
```

Continuation prompt:

```text
Continue the studio workflow.
```

The coordinator should inspect existing artifacts and proceed to the next state
without asking the user to name the tier or role.

Good prompt:

```text
Use the Codex development studio for Brawler Heroes.
Run Tier 1 only. Use product-lead.
Create a run log and a product brief.
Do not implement code until I approve the brief.
```

Use direct Tier prompts only when you already know the current stage. Otherwise,
start with `/start`.

Good prompt for the next stage:

```text
Tier 1 is approved.
Run Tier 2 with ux-designer, data-api-engineer, and seo-content-specialist.
Create separate run logs and briefs.
Do not implement code yet.
```

Good prompt for implementation:

```text
Tier 2 is approved.
Run Tier 3 implementation for the approved V1 scope.
Use frontend-engineer for UI and data-api-engineer for seed data.
Record changed files in the run logs.
```

Good prompt for verification:

```text
Run Tier 4 verification.
Use qa-tester and performance-reviewer.
Create QA and performance reports before final summary.
```

## When To Use Sub-Agents

Use sub-agents when the user explicitly asks for:

- multi-agent work
- parallel roles
- delegation
- separate agent outputs

The coordinator may do small single-role work directly, but then it must say so
clearly in the run log. If the user wants proof that each role worked
independently, spawn separate agents for those roles.

## What Good Studio Output Looks Like

Bad output:

```text
I made the site. Here is the summary.
```

Good output:

```text
Tier 1 product-lead completed.
Run log: docs/studio-runs/2026-05-27-tier-1-product-lead.md
Artifact: docs/product-lead-brief.md
Status: awaiting approval before Tier 2.
```

Good implementation output:

```text
Tier 3 frontend-engineer completed.
Run log: docs/studio-runs/2026-05-27-tier-3-frontend-engineer.md
Changed files:
- src/app/[locale]/page.tsx
- src/app/[locale]/brawlers/page.tsx
- src/components/brawler-browser.tsx
Verification still pending Tier 4.
```

## Why This Helps

The benefit of the studio is not that it sounds like a company. The benefit is:

- fewer hidden decisions
- less scope creep
- better handoffs
- easier review
- clear separation between planning and implementation
- visible accountability for each role

If those benefits are not visible in the files, the studio is not being used
correctly.
