# Active Session State

## Current Goal

Create a Codex-friendly studio layer for building a Brawl Stars website while
preserving the original Claude Code Game Studios files.

## Decisions

- Keep `.claude/` unchanged for Claude Code compatibility.
- Add `.codex-studio/` for Codex role prompts, workflows, rules, and state.
- Start with a lean seven-role website studio instead of porting all game
  development agents.

## Active Roles

- product-lead
- ux-designer
- frontend-engineer
- data-api-engineer
- seo-content-specialist
- qa-tester
- performance-reviewer

## Changed Files

- `.codex-studio/README.md`
- `.codex-studio/agents/*.md`
- `.codex-studio/workflows/*.md`
- `.codex-studio/rules/*.md`
- `.codex-studio/session-state/active.md`

## Open Questions

- Should this remain Brawl Stars specific, or become a reusable website studio
  template with Brawl Stars as one preset?
- Should `.claude/` later be adapted too, or should Codex and Claude workflows
  stay separate?

## Next Suggested Work

- Add a root README section pointing to `.codex-studio/`.
- Add a reusable prompt for starting multi-agent feature work.
- Optionally create `.codex-studio/workflows/start-project.md`.

