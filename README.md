🌱 Village API — Rural Data & Administration Platform

<p align="center"><strong>India Village Data API + Admin Dashboard</strong><br>A full-stack platform for accessing, searching, managing and monitoring village-level location data.</p>

     

📌 Project Overview

Village API is a full-stack B2B platform for structured Indian village and administrative-location data through secure REST APIs and an administrator dashboard.

Hierarchy: Country → State → District → Sub-district → Village

The platform combines a FastAPI backend, React + TypeScript + Vite frontend, PostgreSQL/NeonDB, Redis-supported services, JWT authentication, API-key authentication, Alembic migrations, analytics and administration tools.

✨ Key Features

🗺️ Location Hierarchy

State → District → Sub-district → Village navigation

Village search, filtering and pagination

Village code and administrative metadata

🔎 Quick Search

Search across village name/code, sub-district name/code, district name/code and state name/code.

📊 Admin Dashboard

Total villages

Active users

API requests

Average response time

Villages by state

API request trends

Usage analytics

👥 User Management

Administrators can search, filter, view, approve, suspend, activate and delete users, inspect user-specific API keys and request history, and manage state access.

🔑 API Key Management

Create, activate, revoke and rotate API keys; configure rate limits; view request counts; and associate keys with users.

📜 API Logs

View timestamp, API key, method, endpoint, response status, response time and IP information. Supports search, filtering, pagination and CSV export.

🏗️ Architecture

Admin User
    ↓
React + TypeScript Admin Dashboard
    ↓ REST API
FastAPI Backend
    ├── PostgreSQL / NeonDB
    └── Redis

🛠️ Technology Stack

Layer

Technologies

Frontend

React, TypeScript, Vite, Tailwind CSS, Recharts, Zustand, TanStack React Query

Backend

Python, FastAPI, SQLAlchemy, Uvicorn

Database

PostgreSQL, NeonDB

Migrations

Alembic

Supporting services

Redis

Authentication

JWT, API Key + API Secret

📁 Project Structure

Village_API/
├── README.md
├── .gitignore
├── backend/
│   ├── app/
│   ├── alembic/
│   ├── dataset/
│   ├── scripts/
│   ├── tests/
│   ├── templates/
│   ├── .env.example
│   ├── Dockerfile
│   ├── main.py
│   ├── pyproject.toml
│   └── alembic.ini
└── frontend/
    ├── public/
    ├── src/
    ├── .env.example
    ├── package.json
    ├── tsconfig.json
    └── vite.config.ts

🚀 Getting Started

Prerequisites

Python 3.x

Node.js and npm

PostgreSQL/NeonDB

Redis where required by the configured backend services

Git

Backend

cd backend
python -m venv .venv

Windows:

.venv\Scripts\activate

macOS/Linux:

source .venv/bin/activate

Install the project's backend dependencies according to its Python configuration, then create backend/.env using backend/.env.example.

Typical required configuration includes:

DATABASE_URL=your_postgresql_connection_string
SECRET_KEY=your_secret_key
REDIS_URL=your_redis_connection_string

Run:

uvicorn main:app --reload --port 8000

Backend: http://127.0.0.1:8000

Swagger / OpenAPI

Swagger UI: /docs

ReDoc: /redoc

OpenAPI JSON: /openapi.json

Frontend

cd frontend
npm install
npm run dev

Create frontend/.env from frontend/.env.example:

VITE_API_BASE_URL=http://localhost:8000/api/v1
VITE_API_KEY=your_demo_api_key
VITE_API_SECRET=your_demo_api_secret
VITE_DEMO_EMAIL=demo@example.com
VITE_DEMO_PASSWORD=your_demo_password

VITE_* values are bundled into the browser application. Do not place master/private production secrets in the frontend. Use dedicated restricted credentials for dashboard/demo access and never commit the real .env file.

🔄 Authentication Flow

Email + Password
       ↓
POST /auth/login
       ↓
JWT access token
       ↓
GET /auth/me
       ↓
Admin verification
       ↓
Admin Dashboard

API consumers authenticate with X-API-Key and X-API-Secret according to the configured backend security rules.

📚 Main API Areas

/auth/login
/auth/me
/states
/districts
/subdistricts
/villages
/autocomplete
/search
/admin/users
/admin/keys
/admin/logs
/admin/usage
/admin/overview
/analytics/summary
/analytics/request-trend
/analytics/top-states

Use /docs as the authoritative source for the exact current endpoints, parameters and schemas.

🗄️ Database

Major data areas include:

users
api_keys
request_logs
countries
states
districts
sub_districts
villages
user_state_access
alembic_version

The current project dataset contains approximately 564K village records.

Migrations

alembic current
alembic upgrade head

For a new migration:

alembic revision --autogenerate -m "describe change"

Always review generated migrations before applying them to production.

🧪 Functional Verification

The main workflows have been verified during development:

Login/authentication

Dashboard

Quick village search

Village browser

User management

API key management

API logs

Settings

State access management

User-scoped API keys and request history

API key rotation

Swagger/OpenAPI

🌐 Deployment

Recommended deployment architecture:

Frontend → Vercel / equivalent frontend hosting
Backend  → Render / equivalent Python hosting
Database → Neon PostgreSQL
Redis    → Managed Redis / equivalent service

Production checklist:

[ ] Real .env files are not committed
[ ] Production secrets are stored in hosting environment variables
[ ] Dedicated demo/admin account is used
[ ] Master API secrets are not exposed in frontend code
[ ] Backend CORS allows only the deployed frontend origin
[ ] API keys have appropriate rate limits
[ ] Database migrations are applied
[ ] /docs is reachable as intended
[ ] Authentication and API requests work after deployment

👥 Team

This project was developed collaboratively.

Team Member

Primary Responsibility

Priya Singh

Backend development, FastAPI, REST APIs, authentication and backend integration

Vinay

Database and data engineering, village data preparation/import and database work

Darshan B

Frontend development, React dashboard, UI/UX and frontend-backend integration

Contribution Areas

Priya Singh — Backend

FastAPI backend and REST APIs

Authentication and backend architecture

Database/API integration

API administration

Vinay — Database & Data

Village/location dataset

Database preparation and data import

PostgreSQL/NeonDB work

Data foundation

Darshan B — Frontend & Integration

React + TypeScript frontend

Admin dashboard and UI/UX

Location hierarchy and Quick Search

User management, API keys and API logs interfaces

Frontend/backend integration

Add GitHub and LinkedIn links beside each team member if everyone agrees to publish them.

📈 Future Enhancements

Advanced analytics

Granular API usage controls

Billing/subscription integration

More detailed API consumer documentation

Caching and query optimization

Granular role-based administration

Production monitoring and alerting

Automated CI/CD

📄 License

Add the project's chosen license before public release. Do not add a license unless the project owners have agreed to it.

<p align="center"><strong>Village API</strong><br>Rural Data • Secure APIs • Real Impact</p>