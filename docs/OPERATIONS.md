# Operations Runbook

## Health Probes

1. Liveness: `GET /health`
2. Readiness: `GET /ready`
3. Liveness alias: `GET /healthz`
4. Readiness alias: `GET /readyz`

## Suggested Alerts

1. Liveness failures for 2+ minutes.
2. 5xx response rate above 2% over 5 minutes.
3. Rate-limited traffic spikes (`429`) indicating abusive or misconfigured clients.
4. Unexpected loss of `X-Request-ID` header in API responses.
5. Sudden drop in average final score across top-ranked models.

## Incident Triage

1. Determine whether issue is API availability, scoring logic, or data quality.
2. Check recent runs and compare against prior leaderboard baseline.
3. Confirm provider fallback notes for requested external evaluators.
4. Roll back recent model/prompt changes if score regressions are confirmed.
5. Document root cause and add regression tests.

## Backup and Recovery

- SQLite file at `LLM_JUDGE_DB_PATH` contains run history.
- Back up the data volume on a schedule.
- Restore by replacing DB file and restarting backend.

## Capacity Notes

- v0.1.0 scoring is CPU-bound deterministic logic.
- Scale backend horizontally behind a load balancer.
- Move to managed Postgres when multi-writer concurrency is needed.
