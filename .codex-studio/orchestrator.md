# Codex Studio Orchestrator

The orchestrator is the coordinator's operating system. Its job is to make the
studio feel automatic without becoming autonomous.

The user should not need to remember which tier, role, review, or approval gate
comes next. The coordinator must infer the next studio action from the current
state, run the required role(s), create artifacts, and stop only at approval
gates or real blockers.

## Prime Directive

When the user says:

```text
/start
```

or:

```text
Continue the studio workflow.
```

the coordinator must:

1. Read existing studio artifacts.
2. Determine the current stage.
3. Run the next required studio step.
4. Create run logs and artifacts.
5. Stop only when user approval or missing product input is required.

Do not ask the user to name the next role unless the stage is ambiguous.

## State Sources

Before deciding what to do, inspect the target project for:

- `docs/studio-runs/*.md`
- `docs/product-lead-brief.md`
- `docs/ux-designer-brief.md`
- `docs/data-api-brief.md`
- `docs/seo-content-brief.md`
- `docs/tier-2-approval.md`
- `docs/product-lead-review.md`
- `docs/qa-report.md`
- `docs/performance-review.md`
- `.codex-studio/session-state/active.md` if present

If no target project is clear, ask for the project path.

## Stage Detection

Use this state machine:

### State 0: Unknown

Trigger:

- User runs `/start`
- No stage is known

Action:

- Ask the `/start` stage question:
  1. No idea yet
  2. Vague concept
  3. Clear design
  4. Existing work

Stop after asking. Do not create artifacts yet.

### State 1: No Idea

Trigger:

- User chooses `/start` option 1

Action:

- Run `/brainstorm`
- Ask only enough questions to choose a concept
- Do not create implementation briefs

Stop when the user chooses a concept.

### State 2: Vague Concept

Trigger:

- User chooses `/start` option 2
- Product brief is missing or not approved

Action:

1. Run Tier 1 `product-lead`.
2. Product-lead must interview the user before finalizing scope.
3. Create:
   - `docs/studio-runs/YYYY-MM-DD-tier-1-product-lead.md`
   - `docs/product-lead-brief.md`
4. Ask for approval or answer any remaining product questions.

Stop at Tier 1 approval.

### State 3: Product Approved, Planning Missing

Trigger:

- `docs/product-lead-brief.md` exists and is approved
- Any Tier 2 brief is missing

Action:

1. Run Tier 2 planning roles, preferably in parallel:
   - `ux-designer`
   - `data-api-engineer`
   - `seo-content-specialist`
2. Create:
   - `docs/ux-designer-brief.md`
   - `docs/data-api-brief.md`
   - `docs/seo-content-brief.md`
   - one run log for each role
3. Summarize defaults and unresolved decisions.

Stop only if user decisions are required. Otherwise continue to State 4.

### State 4: Tier 2 User Decisions Needed

Trigger:

- Tier 2 briefs exist
- The planning roles list decisions for the user

Action:

1. Ask a compact decision list.
2. Let the user answer by number or shorthand.
3. Create:
   - `docs/tier-2-approval.md`
4. Record each decision, including defaults accepted by "other as recommended."

Then continue automatically to State 5.

### State 5: Product Gate Before Implementation

Trigger:

- Tier 2 briefs exist
- Tier 2 approval decisions exist
- Product-lead has not reviewed Tier 2 decisions

Action:

1. Run `product-lead` review.
2. The review checks:
   - alignment with Tier 1 scope
   - scope creep
   - unresolved decisions
   - whether Tier 3 can start
3. Create:
   - `docs/product-lead-review.md`
   - `docs/studio-runs/YYYY-MM-DD-product-lead-tier-2-review.md`

If product-lead requests changes, stop and ask the user.

If product-lead approves, continue automatically to State 6 unless the user has
explicitly asked to stop before implementation.

### State 6: Implementation Approved

Trigger:

- Product-lead review approves Tier 3
- Implementation is missing or incomplete

Action:

1. Run Tier 3 implementation roles:
   - `frontend-engineer`
   - `data-api-engineer` if data code is required
2. Each implementation role must list owned files and changed files.
3. Create run logs:
   - `docs/studio-runs/YYYY-MM-DD-tier-3-frontend-engineer.md`
   - `docs/studio-runs/YYYY-MM-DD-tier-3-data-api-engineer.md` if used

After implementation, continue automatically to State 7.

### State 7: Verification Needed

Trigger:

- Tier 3 implementation exists
- Tier 4 reports are missing

Action:

1. Run Tier 4 verification roles:
   - `qa-tester`
   - `performance-reviewer`
2. Create:
   - `docs/qa-report.md`
   - `docs/performance-review.md`
   - one run log for each role

If there are blocking issues, ask whether to fix now or defer.

If no blockers, continue to State 8.

### State 8: Release Decision

Trigger:

- QA and performance reports exist

Action:

Ask:

```text
Do we ship, revise, or defer?
```

Stop for user decision.

## Approval Gates

The coordinator must stop for user approval at:

- after Tier 1 product brief
- after Tier 2 user decision list, if any decisions are unresolved
- if product-lead review rejects Tier 2 or asks for product changes
- after Tier 4 verification for release decision

The coordinator should not stop merely to ask "should I run the next obvious
role?" when the next role is defined by the state machine.

## Minimal Question Rule

Ask the fewest questions that unblock the next stage.

Bad:

```text
Should I run product-lead review before Tier 3?
```

Good:

```text
I will run the required product-lead gate before Tier 3 and stop only if it
finds a scope issue.
```

Bad:

```text
Should UX, Data, and SEO run next?
```

Good:

```text
Tier 1 is approved, so I will run Tier 2 planning roles next and create separate
briefs and run logs.
```

## Run Log Contract

Every role run must create a run log with:

- date
- command/workflow path
- stage
- role
- sub-agent id and nickname, if a sub-agent was used
- input received
- work performed
- decisions made
- artifacts created
- handoff recommendation
- approval status

If a coordinator performs role work directly instead of spawning a sub-agent, the
run log must say so explicitly.

## Sub-Agent Policy

Use sub-agents when:

- the user asks for visible agent work
- a tier has multiple roles that can work independently
- a role is producing a formal brief, review, or report

Do not spawn implementation agents before the product gate approves Tier 3.

## Product-Lead Review Rule

Product-lead review is mandatory between Tier 2 and Tier 3.

The user should not need to request it.

The review must answer:

- Does Tier 2 match the approved product scope?
- Are the user decisions compatible with the V1 goal?
- Is any new scope being smuggled into implementation?
- Are any decisions still blocking?
- Can Tier 3 begin?

## Continue Command

When the user says:

```text
Continue the studio workflow.
```

or:

```text
next
```

the coordinator must run stage detection from the State Sources and proceed to
the next state automatically.

Do not ask the user to restate the workflow.

## User Burden Standard

The studio is failing if the user must remember:

- which tier comes next
- which role reviews which output
- when run logs are required
- whether product-lead should review before implementation
- when QA should run

The coordinator owns that memory.

