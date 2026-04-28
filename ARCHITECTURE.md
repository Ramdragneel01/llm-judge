# llm-judge Architecture

## 1. System Overview

llm-judge is a two-service platform:

1. Backend API (FastAPI): run orchestration, scoring pipeline, persistence, leaderboard aggregation.
2. Frontend Dashboard (React): run submission, result triage, leaderboard visualization.

The system is stateless at API layer and stateful at storage layer via SQLite for easy portability.

## 2. Backend Layers

1. API Layer (`backend/app/main.py`)
- HTTP endpoints
- Input validation and response shaping
- Health and readiness probes

2. Service Layer (`backend/app/service.py`)
- Run execution orchestration
- Judge provider selection
- Aggregation and persistence handoff

3. Scoring Layer (`backend/app/scoring.py`)
- Deterministic baseline metrics
- Weighted final score computation
- Safety and hallucination risk handling

4. Provider Layer (`backend/app/providers.py`)
- Provider adapter contracts
- Fallback from unavailable external providers to local judge

5. Storage Layer (`backend/app/store.py`)
- SQLite schema creation and migrations (v0 baseline)
- Run inserts and leaderboard queries

## 3. Frontend Layers

1. Submission panel for evaluation payloads.
2. Run summary cards for quick signal.
3. Leaderboard table for model-level comparison.

## 4. Security Controls

1. Payload size guard middleware.
2. Trusted host filtering.
3. CORS allowlist.
4. Optional HSTS in production.
5. Input constraints on prompt, response, and identifier fields.
6. Provider key checks before external judge selection.

## 5. Deployment Model

1. Local compose for development.
2. Production compose profile with restart policies.
3. GitHub Actions CI (tests + frontend build + compose validation).
4. Release workflow for GHCR images.
5. GitHub Pages workflow for static dashboard deployment.

## 6. Operational Model

1. Liveness and readiness probes.
2. Structured run history persisted in SQLite.
3. Alert strategy documented in docs/OPERATIONS.md.
4. Clarification notes preserved in docs/FUTURE-CLARIFICATIONS.md.
