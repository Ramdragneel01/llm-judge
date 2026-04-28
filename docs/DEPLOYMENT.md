# Deployment Guide

## Local Deployment

1. Copy environment file:

```bash
cp .env.example .env
```

2. Launch stack:

```bash
docker compose --env-file .env up --build
```

3. Validate:
- Dashboard: http://localhost:8090
- API docs: http://localhost:8010/docs
- Health: http://localhost:8010/health

## Production Deployment

Use the service Dockerfiles:

- `backend/Dockerfile`
- `frontend/Dockerfile`

Recommended topology:

1. Public frontend service.
2. Private backend service behind ingress.
3. TLS termination at gateway/load balancer.
4. Persistent volume for SQLite data path.

## GHCR Release Flow

Tag pushes trigger image publish from `.github/workflows/release.yml`:

- `ghcr.io/<owner>/llm-judge-backend:<tag>`
- `ghcr.io/<owner>/llm-judge-frontend:<tag>`

Tag example:

```bash
git tag v0.1.0
git push origin v0.1.0
```

## GitHub Pages

The frontend can be deployed statically with `.github/workflows/pages.yml`.

Note:
- GitHub Pages is static-only.
- Set repository variable `LLM_JUDGE_API_BASE_URL` to the hosted backend URL.

## Environment Variables

Backend:

- `LLM_JUDGE_ENV`
- `LLM_JUDGE_ALLOWED_HOSTS`
- `LLM_JUDGE_CORS_ORIGINS`
- `LLM_JUDGE_MAX_PAYLOAD_BYTES`
- `LLM_JUDGE_GZIP_MINIMUM_SIZE`
- `LLM_JUDGE_ENABLE_HSTS`
- `LLM_JUDGE_PORT`
- `LLM_JUDGE_DB_PATH`
- `LLM_JUDGE_RATE_LIMIT_PER_MINUTE`
- `LLM_JUDGE_STRICT_PROVIDER`
- `OPENAI_API_KEY`
- `ANTHROPIC_API_KEY`
- `GEMINI_API_KEY`

Frontend:

- `VITE_API_BASE_URL`
