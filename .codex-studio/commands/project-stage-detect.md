# Command: /project-stage-detect

Use this command when there is already a project, repository, document set, or
partial implementation.

## Goal

Understand the current state before choosing a workflow.

## Process

1. Inspect the repo or project files.
2. Identify the stack, routes, data model, existing docs, and current gaps.
3. Check whether prior studio artifacts exist:
   - product brief
   - UX brief
   - data/API brief
   - SEO/content brief
   - QA or performance reports
   - studio run logs
4. Classify the project stage:
   - no product scope
   - product scope exists, planning missing
   - planning exists, implementation missing
   - implementation exists, verification missing
   - verification complete, ready for release decision
5. Recommend the next command or workflow.

## Output

Create or update:

```text
docs/studio-runs/YYYY-MM-DD-project-stage-detect.md
```

The report should include:

- files inspected
- current stage
- missing artifacts
- recommended next workflow
- risks

## Rules

- Do not implement code.
- Do not rewrite existing files except the stage detection report.
- Do not assume the user wants to continue until they approve the recommendation.

