# API Reference

## System Endpoints

1. `GET /health`
- Returns `{ "status": "ok" }`.

2. `GET /ready`
- Returns `{ "status": "ready" }` when API and storage are available.

3. `GET /healthz`
- Compatibility alias for `/health`.

4. `GET /readyz`
- Compatibility alias for `/ready`.

## Evaluation Endpoints

1. `POST /api/v1/evals/run`
- Runs evaluation for the provided prompt/response pairs.
- Persists run and item-level scores.

Request shape (summary):
- `run_name`: string
- `judge_provider`: `local | openai | anthropic | gemini`
- `judge_model`: string
- `items`: list of prompt-response items
- `dimension_weights`: optional dictionary

2. `GET /api/v1/evals/runs?limit=25`
- Returns recent runs with metadata and average score.

3. `GET /api/v1/evals/leaderboard?limit=20`
- Returns model/provider aggregate performance rankings.

## Error Behavior

- `400` for invalid runtime constraints.
- `413` when payload exceeds configured max size.
- `422` for schema validation failures.
- `429` for rate-limited traffic.

Error payload envelope:

```json
{
	"error": {
		"code": "rate_limited",
		"message": "rate_limited",
		"request_id": "f6aafcd2-25f2-4f5e-b0f6-c7446199758f"
	}
}
```
