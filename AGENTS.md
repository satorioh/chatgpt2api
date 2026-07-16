# Repository Guidelines

## Project Structure & Module Organization

The FastAPI backend starts in `main.py`. HTTP handlers live in `api/`; business logic, upstream integrations, protocol adapters, and storage backends live in `services/`. Shared helpers belong in `utils/`, while maintenance utilities are under `scripts/`. Backend tests are in `test/`. The Next.js frontend is isolated in `web/`, with routes in `web/src/app`, reusable components in `web/src/components`, client utilities in `web/src/lib`, and static assets in `web/public`. Deployment notes belong in `docs/`.

## Build, Test, and Development Commands

- `uv sync`: install Python 3.13 dependencies from `uv.lock`.
- `uv run main.py`: run the backend locally with Uvicorn.
- `uv run python -m unittest discover -s test -p 'test_*.py'`: run the backend test suite.
- `cd web && bun install && bun run dev`: install frontend dependencies and start Next.js development mode.
- `cd web && bun run build`: type-check and create the production frontend build.
- `cd web && bunx eslint .`: run the configured Next.js/TypeScript lint rules.
- `docker compose -f docker-compose.local.yml up --build`: build and run the local container stack on port 8000.

## Coding Style & Naming Conventions

Use four-space indentation, type hints, `snake_case` functions, and `PascalCase` classes in Python. Keep route handlers thin and move reusable behavior into focused service modules. TypeScript uses two spaces, double quotes, semicolons, `PascalCase` React components, and `useXxx` hook names. Follow the existing ESLint configuration; avoid introducing a new formatter or lint rule in unrelated changes.

## Testing Guidelines

Tests use Python `unittest` conventions and are named `test/test_<feature>.py`. Name methods `test_<behavior>`, isolate filesystem state with temporary directories, and mock network calls. Cover API response shapes, configuration fallbacks, storage behavior, and failure paths. Run the backend suite and frontend build before submitting cross-stack changes.

## Commit & Pull Request Guidelines

Recent history favors Conventional Commit prefixes such as `feat:`, `fix:`, `refactor:`, `docs:`, and scoped forms like `fix(register):`. Keep each commit focused and use an imperative summary. Pull requests should explain user-visible impact, list verification commands, link relevant issues, and include screenshots for frontend changes. Call out configuration or migration steps explicitly.

## Security & Configuration

Never commit real tokens, account exports, proxy credentials, database files, or generated `data/`. Treat `config.json` and `.env` values as secrets; use placeholders in examples and document new environment variables in the deployment docs.
