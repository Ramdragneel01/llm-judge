# Future Clarification Notes

This file captures intentional trade-offs and design comments for future contributors.

## Current Decisions

1. v0.1.0 uses deterministic local scoring so evaluations are reproducible in CI.
2. External provider keys are accepted, but provider-native judge adapters are intentionally deferred.
3. SQLite is used first for low-friction deployment and easy local reproducibility.

## Planned Clarifications to Add in Future PRs

1. When adding provider-native judge adapters, document scoring variance expectations.
2. When changing default weights, include historical leaderboard impact analysis.
3. When moving from SQLite to Postgres, document migration and rollback strategy.

## Why This Matters

- Prevents silent behavior drift in scoring logic.
- Keeps recruiter-facing repo quality high with explicit rationale.
- Preserves context for reviewers and future maintainers.
