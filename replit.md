# Научный навигатор

Рабочая основа русскоязычной системы сопровождения исследователя от научной идеи к готовому результату.

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

- `artifacts/scientific-navigator` — исследовательский интерфейс и маршруты приложения.
- `artifacts/api-server` — общий API-сервер; подключать к научным модулям только после определения реальных источников и контрактов.
- `lib/api-spec/openapi.yaml` — источник истины для будущих API-контрактов.
- `lib/db/src/schema/` — место для будущих моделей хранения проектов, когда для них появится серверная персистентность.

## Architecture decisions

- Отделять подготовленные интерфейсы будущих модулей от доступных функций: неподключённый поиск или анализ не должен выглядеть как работающий.
- Научные публикации, тренды, пробелы, журналы и гранты показывать только после подключения проверяемых источников; не подменять их демонстрационными записями.
- Пользовательский черновик идеи допустимо сохранять локально до появления серверного хранения, но явно сообщать область хранения и то, что научный анализ не выполнялся.

## Product

Приложение помогает организовать путь исследователя: сформулировать идею, продолжить собственные проекты, а в будущем — искать темы и источники, анализировать литературу и готовить научные работы и публикации. Первая версия — интерфейс и честные страницы будущих модулей; подключение научных данных и AI выполняется отдельными этапами.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- Не добавлять фиктивные результаты, метрики, статьи, тренды, проекты, рекомендации или активность для заполнения интерфейса.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
