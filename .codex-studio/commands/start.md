# Command: /start

Use this command when the user wants to begin using the development studio but
has not chosen a workflow yet.

Read `../orchestrator.md` before acting. `/start` is the entry point into the
orchestrator state machine.

Do not assume the project stage. Ask where the user is, then route them to the
right workflow.

## First Response

Ask:

```text
Where are you right now?

1. No idea yet
   You want to explore possible project directions.

2. Vague concept
   You know the rough product or audience, but not the scope.

3. Clear design
   You know what to build and need planning / implementation.

4. Existing work
   There is already a codebase or content that needs analysis.
```

Do not create a product brief yet. Do not spawn implementation agents yet. Wait
for the user's answer.

## Routing

After the user answers, route as follows:

### 1. No idea yet

Use:

- `/brainstorm`

Goal:

- explore possible directions
- identify audience
- pick one promising project concept

Do not create implementation plans.

### 2. Vague concept

Use:

- `workflows/start-project.md`
- Tier 1 `product-lead`

Goal:

- interview the user
- define product positioning
- define V1 scope
- define non-goals and acceptance criteria

Required artifacts:

- `docs/studio-runs/YYYY-MM-DD-tier-1-product-lead.md`
- `docs/product-lead-brief.md`

### 3. Clear design

Use:

- Tier 2 planning roles if product scope is already approved
- `workflows/build-feature.md` if feature scope is already approved

Goal:

- convert approved scope into UX, data, SEO, and implementation briefs

Do not implement until planning artifacts are approved.

### 4. Existing work

Use:

- `/project-stage-detect`

Goal:

- inspect the existing repo
- identify what already exists
- recommend the correct next workflow

Do not rewrite or implement before reporting findings.

## Completion

`/start` is complete only when it has routed the user to the next command or
workflow.

It should not produce final product artifacts by itself.
