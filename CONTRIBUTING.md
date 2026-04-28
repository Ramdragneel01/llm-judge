# Contributing to llm-judge

## Development Prerequisites

- Python 3.12+
- Node.js 20+
- Docker (optional but recommended)

## Local Development

1. Backend:

```bash
cd backend
python -m venv .venv
. .venv/Scripts/activate
pip install -r requirements.txt
pytest -q
uvicorn app.main:app --reload --host 0.0.0.0 --port 8010
```

2. Frontend:

```bash
cd frontend
npm install
npm run dev -- --host --port 8090
```

## Pull Request Expectations

1. Include tests for behavior changes.
2. Keep security and accessibility constraints intact.
3. Update docs/FUTURE-CLARIFICATIONS.md for non-obvious trade-offs.
4. Keep CHANGELOG.md updated for user-visible changes.
