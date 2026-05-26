# Workflow: Build Feature

Use this workflow for a new website feature such as brawler search, build
comparison, event listing, tier list filtering, map guides, or player lookup.

## Steps

1. `product-lead` defines the user story, acceptance criteria, and non-goals.
2. `ux-designer` defines the route, page sections, states, and mobile behavior.
3. `data-api-engineer` defines required data, source, schema, cache, and failure
   behavior.
4. `frontend-engineer` implements UI and connects data contracts.
5. `seo-content-specialist` reviews metadata, headings, and internal links.
6. `qa-tester` verifies the feature across expected states and viewports.
7. `performance-reviewer` checks rendering, network, and layout stability.
8. The coordinator updates `session-state/active.md`.

## Parallelization

When explicitly using multi-agent work, split independent tasks:

- UX and product can work first or together.
- Frontend and data can run in parallel only after the contract is clear.
- SEO, QA, and performance should run after implementation, unless they are
  reviewing a design or plan.

## Completion Criteria

- Acceptance criteria are satisfied.
- Data failure states do not break the UI.
- Mobile layout is usable.
- Tests or manual verification are recorded.
- Session state is updated.

