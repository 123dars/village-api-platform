# India Location Data API

A production-ready, FastAPI-based B2B API platform providing structured access to All India villages, sub-districts, districts, and states data. Built with SQLAlchemy, FastAPI, pandas, and PostgreSQL, it offers secure API-key-protected endpoints for address forms, dropdown menus, KYC systems, and logistics/delivery platforms.

## Features

- Normalized PostgreSQL database (states, districts, sub-districts, villages)
- Secure API key **& secret** access (rate-limited, rotating HMAC-backed secrets)
- JWT-based dashboard authentication (the first signed-up user becomes the admin)
- Admin routes for key management, usage analytics, request logs, and user management
- High-performance search and filtering endpoints
- Data analysis / analytics endpoints
- Structured logging (console + rotating file) and per-request usage capture

## Getting Started

This is a `uv` Python project.

```bash
# Install dependencies
uv add .

# Apply schema migrations
uv run alembic upgrade head

# Load seed data from the Census 2011 dataset folder (30 files, ~564K villages)
uv run python scripts/seed_data.py

# Run the API server
uv run uvicorn app.main:app --reload

# Lint
uv run ruff check app/ tests/ scripts/

# Run the test suite
uv run pytest tests/ -q
```

## API Keys & Secrets

Create a key with a no-auth POST — every new key ships with a **secret** that is only
shown once and must be sent as `X-API-Secret` on every call:

```bash
curl -X POST http://localhost:8000/api/v1/keys/generate \
  -H "Content-Type: application/json" \
  -d '{"name": "my-client", "rate_limit": 1000}'
```

Then use it:

```bash
curl http://localhost:8000/api/v1/states \
  -H "X-API-Key: bol_xxx" \
  -H "X-API-Secret: my-secret"
```

## Dashboard Authentication

The first account created through `POST /api/v1/auth/signup` is promoted to admin
automatically. Admin endpoints live under `/api/v1/admin/*` and require a bearer token:

```bash
curl -X POST http://localhost:8000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "admin@example.com", "password": "..."}'
```

| Endpoint                  | Description                                     |
| ------------------------- | ----------------------------------------------- |
| `GET /admin/overview`     | Dashboard stats, usage summary, recent logs     |
| `GET /admin/keys`         | List all API keys                               |
| `POST /admin/keys`        | Create a key (returns secret once)              |
| `PATCH /admin/keys/{id}`  | Activate/revoke, change rate limit              |
| `GET /admin/usage`        | Hourly/daily request volumes                    |
| `GET /admin/logs`         | Filterable request log                          |
| `GET /admin/logs/top-clients` | Busiest API keys                             |
| `GET /admin/users`        | Dashboard users                                 |

## Environment

Copy `.env.example` to `.env` and set at minimum `DATABASE_URL`. `JWT_SECRET` should
be a long random value in production.