# Weather Bot Dashboard

A React dashboard and Python Telegram bot for querying global weather by coordinates and date or year, with request history and operational logs.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/weather-bot/` — React operations dashboard and Python FastAPI/Telegram service
- `artifacts/weather-bot/backend/` — weather provider, bot, database, and dashboard API
- `lib/api-spec/openapi.yaml` — dashboard API contract

## Architecture decisions

- The dashboard and bot share a Python service so weather queries and operational records use the same implementation.
- Past periods are returned as historical observations; dates beyond Visual Crossing's forecast horizon are rejected rather than presented as forecasts.

## Product

- Telegram users can query temperature, humidity, dew point, and daily conditions using latitude, longitude, and an ISO date or year.
- Operators can run manual queries and review request history, service health, and bot logs in the web dashboard.

## User preferences


## Gotchas

- The Python service requires `VISUAL_CROSSING_API_KEY`, `TELEGRAM_BOT_TOKEN`, and the workspace `DATABASE_URL`.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
