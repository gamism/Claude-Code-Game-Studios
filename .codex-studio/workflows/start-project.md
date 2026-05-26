# Workflow: Start Project

Use this workflow when starting a new website, rebooting a stale project, or
turning a loose idea into an actionable first release.

## Inputs

Collect only what is needed to begin:

- Project name
- Target users
- Primary player problem
- Must-have pages or workflows
- Data sources and API constraints
- Launch target or deadline, if any
- Known tech stack or hosting constraints

If an input is unknown, record it as an open question instead of blocking the
whole project.

## Steps

1. `product-lead` writes the project brief:
   - audience
   - core promise
   - first release scope
   - non-goals
   - acceptance criteria
2. `ux-designer` proposes the first information architecture:
   - primary routes
   - navigation model
   - key user flows
   - mobile-first layout risks
3. `data-api-engineer` maps the data plan:
   - required entities
   - source of truth
   - cache and freshness expectations
   - missing or risky data
4. `seo-content-specialist` defines the content and search plan:
   - indexable page types
   - page intent
   - metadata pattern
   - internal linking model
5. `frontend-engineer` identifies the implementation skeleton:
   - app structure
   - shared components
   - route templates
   - immediate technical risks
6. `qa-tester` drafts the first test checklist.
7. `performance-reviewer` flags early speed and rendering risks.
8. The coordinator updates `session-state/active.md`.

## First Release Shape

Prefer a small release that proves the website is useful:

- One useful homepage or dashboard, not a marketing placeholder.
- One complete content or data page template.
- One search, filter, or lookup flow if the project depends on discovery.
- Clear loading, empty, and error states.
- A short list of deferred work.

## Output

The coordinator should produce:

- Project brief
- First-release scope
- Route and page list
- Data/API plan
- Content/SEO plan
- Implementation plan
- QA checklist
- Performance risks
- Updated `session-state/active.md`

