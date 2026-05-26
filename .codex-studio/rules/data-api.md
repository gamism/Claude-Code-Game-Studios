# Data and API Rules

- Treat external game data as versioned, partial, and occasionally stale.
- Keep API tokens and secrets server-side only.
- Define typed data contracts before wiring large UI surfaces.
- Normalize external payloads at the boundary.
- Document cache duration and freshness expectations.
- Handle missing brawler, map, mode, event, and player fields gracefully.
- Avoid repeated client-side request waterfalls.
- Prefer structured parsers and schemas over ad hoc string handling.

