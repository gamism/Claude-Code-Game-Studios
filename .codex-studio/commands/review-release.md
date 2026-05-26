# Command: /review-release

Use this command when implementation exists and the user wants a release check.

## Routing

Use:

- `workflows/review-release.md`
- `qa-tester`
- `performance-reviewer`

## Required Outputs

- `docs/qa-report.md`
- `docs/performance-review.md`
- run log for each verification role

## Final Release Decision

The coordinator should ask:

```text
Do we ship, revise, or defer?
```

Do not declare the release complete until the user makes that decision.

