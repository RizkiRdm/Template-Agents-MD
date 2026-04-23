# PROJECT CONTEXT

## Overview
- Project name: [NAME]
- Purpose: [ONE SENTENCE — what this project does]
- Status: [active / maintenance / MVP]
- Primary language: [e.g., Python]
- Target environment: [e.g., Linux server / Docker / Vercel]

---

## Tech Stack

### Backend
- Runtime: [e.g., Python 3.11]
- Framework: [e.g., FastAPI 0.111]
- Database: [e.g., PostgreSQL 15]
- ORM: [e.g., SQLAlchemy 2.0]
- Auth: [e.g., JWT via python-jose]

### Frontend (if any)
- Framework: [e.g., Next.js 14]
- Styling: [e.g., Tailwind CSS]
- State: [e.g., Zustand]

### Infrastructure
- Container: [e.g., Docker + Docker Compose]
- CI/CD: [e.g., GitHub Actions]
- Hosting: [e.g., Railway / Render / VPS]

---

## Architecture Overview

[Describe in max 5 bullet points. Be explicit.]

- Pattern: [e.g., Layered Architecture — Router → Service → Repository]
- API style: [e.g., RESTful, versioned under /api/v1]
- Auth flow: [e.g., JWT access token (15m) + refresh token (7d)]
- Background jobs: [e.g., Celery + Redis / None]
- External services: [e.g., Google Gemini API, Midtrans]

---

## Project Structure

```text
src/
├── api/          # Route handlers (thin layer, no business logic)
├── services/     # Business logic
├── repositories/ # DB queries only
├── models/       # DB models / schemas
├── core/         # Config, security, dependencies
└── utils/        # Helpers, shared utilities
tests/
├── unit/
└── integration/
```

---

## Key Commands

```bash
# Install dependencies
[command here]

# Run development server
[command here]

# Run tests
[command here]

# Run linter
[command here]

# Build for production
[command here]

# Database migration
[command here]
```

---

## Coding Conventions

### General
- Language: [e.g., English only — variable names, comments, commit messages]
- Indentation: [e.g., 4 spaces, no tabs]
- Max line length: [e.g., 100 characters]
- File naming: [e.g., snake_case for Python, kebab-case for frontend]

### Naming
- Variables: [e.g., snake_case]
- Classes: [e.g., PascalCase]
- Constants: [e.g., UPPER_SNAKE_CASE]
- Functions: [e.g., snake_case, use verb prefix — get_, create_, validate_]

### Functions & Classes
- Each function MUST do one thing only
- Max function length: 30 lines
- MUST add type hints to all function signatures (Python)
- MUST add JSDoc to all exported functions (JS/TS)

### Error Handling
- NEVER use bare `except:` or `catch (e) {}`
- ALWAYS log errors with context before re-raising
- Use custom exception classes defined in `core/exceptions.py`

---

## API Conventions (if applicable)

- Base URL: `/api/v1`
- Response format:
```json
{
  "success": true,
  "data": {},
  "message": "string"
}
```
- Error format:
```json
{
  "success": false,
  "error": "ERROR_CODE",
  "message": "human readable"
}
```
- HTTP status codes: use semantically correct codes (201 for create, 422 for validation error)

---

## Database Conventions (if applicable)

- Table names: plural, snake_case (e.g., `user_sessions`)
- Primary key: always `id UUID DEFAULT gen_random_uuid()`
- Timestamps: always include `created_at`, `updated_at`
- NEVER write raw SQL in service layer — use repository pattern
- Migrations: MUST be reversible (always write `downgrade()`)

---

## Security Rules

- NEVER hardcode secrets or credentials
- NEVER commit `.env` files
- ALWAYS validate and sanitize user input at the API layer
- NEVER expose stack traces in production responses
- Sensitive config MUST be read from environment variables via `core/config.py`

---

## Testing Rules

- MUST write tests for all service-layer functions
- Test file naming: `test_[module_name].py`
- Use fixtures for DB setup — NEVER hit production DB in tests
- Minimum coverage target: [e.g., 70%]

---

## Git Conventions

- Branch naming: `feature/`, `fix/`, `chore/`, `hotfix/`
- Commit format: `type(scope): short description`
  - Example: `feat(auth): add refresh token rotation`
- NEVER commit directly to `main` or `master`
- PR MUST have a description explaining what and why

---

## AI Agent Rules

> Rules for AI coding assistants reading this file.

### MUST
- Follow the architecture patterns defined above
- Place code in the correct layer (router / service / repository)
- Use existing utilities before creating new ones
- Check existing patterns in the codebase before generating new code

### MUST NOT
- Add new dependencies without noting it explicitly
- Generate inline SQL outside repository layer
- Skip error handling
- Create files outside the defined project structure
- Modify migration files that already exist

### CONTEXT HINTS
- When editing API routes: check `src/api/` for existing patterns
- When adding business logic: it belongs in `src/services/`, not routes
- When writing DB queries: it belongs in `src/repositories/`
- Prefer editing existing files over creating new ones

---

## Known Issues / Gotchas

- [e.g., Redis connection must be initialized before app startup]
- [e.g., Gemini SDK has rate limit — use exponential backoff]
- [Add anything that would trip up an AI or new developer]

---

## Out of Scope

> AI agents MUST NOT do the following without explicit instruction:

- Refactor working code that was not mentioned in the task
- Change database schema without being asked
- Modify `.env.example` or config files
- Add logging to every function (only where specified)
