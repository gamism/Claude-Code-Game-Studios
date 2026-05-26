# Workflow: Review Release

Use this workflow before shipping a meaningful change.

## Gates

1. `qa-tester`: behavior, routes, states, responsive layout, regression risks.
2. `performance-reviewer`: rendering cost, layout shift, images, network.
3. `seo-content-specialist`: metadata, headings, indexability, content accuracy.
4. `product-lead`: confirms scope and decides whether to ship.

## Required Notes

Record the following in `session-state/active.md`:

- What changed
- What was tested
- Known risks
- Deferred follow-up work
- Release decision

