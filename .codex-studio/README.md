# Codex Studio: Brawl Stars Website

This folder adapts the Claude Code Game Studios idea into a Codex-friendly
studio for building a Brawl Stars website.

The original `.claude/` directory is intentionally left untouched. Use it when
working in Claude Code. Use this `.codex-studio/` directory as the shared
operating manual when working with Codex.

## Studio Shape

Start small. The first version uses seven focused roles:

- `product-lead`: scope, priorities, decisions, and release shape
- `ux-designer`: information architecture, page flow, mobile usability
- `frontend-engineer`: Next.js, React, CSS, UI implementation
- `data-api-engineer`: Brawl Stars API, caching, data modeling, sync
- `seo-content-specialist`: guides, metadata, structured content, search
- `qa-tester`: test plans, regression checks, browser and responsive coverage
- `performance-reviewer`: Core Web Vitals, bundle weight, caching, rendering

Codex should treat these as role prompts. A main coordinating agent may spawn
sub-agents only when the task is explicitly multi-agent, parallel, delegated, or
large enough to benefit from independent work.

## Operating Principles

- Keep the live website usable as the first screen; avoid marketing shells.
- Prefer existing project conventions before introducing new architecture.
- Keep user-visible text concise, useful, and easy to translate later.
- Treat API data as unreliable until validated, cached, and rate-limited.
- Save decisions and open questions in `session-state/active.md`.
- Review changes against `rules/` before declaring work complete.

## Default Flow

1. Clarify the feature or problem.
2. Let `product-lead` define the scope and acceptance criteria.
3. Let `ux-designer` shape the interaction and content hierarchy.
4. Let implementation roles work in disjoint areas:
   - `frontend-engineer` owns UI and client behavior.
   - `data-api-engineer` owns API, schemas, cache, and data integrity.
   - `seo-content-specialist` owns metadata and content structure.
5. Run `qa-tester` and `performance-reviewer` as review gates.
6. Update `session-state/active.md` with decisions, changed files, and next work.

## First Workflows

- `workflows/start-project.md`: start a new website or reboot a project
- `workflows/build-feature.md`: build a product feature end to end
- `workflows/create-content-page.md`: create SEO-friendly brawler/map/guide pages
- `workflows/review-release.md`: check quality before shipping

## How To Operate It

Read `USAGE.md` before using the studio on a real project. It defines the
required tier flow, run logs, approval gates, and prompts that make each role's
work visible.
