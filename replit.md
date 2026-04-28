# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.

## ARZAQ PRO ULTRA (artifacts/arzaq)

Arabic RTL mobile-first PWA for sales-commission tracking. Pure frontend, localStorage persistence, emerald/gold palette, Cairo font, framer-motion, shadcn/ui.

### Storage keys
- `arzaq:terms`, `arzaq:users`, `arzaq:currentUser`
- `arzaq:products:v2`
- `arzaq:sales:<username>` — per-user sales (auto-migrated from legacy `arzaq:sales`)
- `arzaq:baseSalary:<username>` — per-user base salary

### Tabs
- **Sales** (all users): live 12-hour clock (visibility-aware, ticks only when tab visible), product picker, quantity (+/-), live commission preview.
- **History**: search, period filters, print report, **permanent fixed legal disclaimer**, delete confirmation showing the operation details (product / company / qty / commission / date+time).
- **Products** (admin only)
- **Admin** (admin only): per-user selector, projected salary = (avg daily commission × 26) + base, recharts bar charts (top company, top product, last-7-days), team leaderboard.
- **Settings**: base salary, Excel import/export (xlsx package — append or replace mode with preview), user management (admin only), support email card (kokanmoh4@gmail.com — clickable mailto + copy), reset all sales (admin), logout.

### Key libs
- `src/lib/store.ts` — types, hooks, per-user storage, admin helpers, `useMigrateLegacyData`
- `src/lib/visibility-clock.ts` — `useVisibilityClock` (no background work) + `formatTime12` ("hh:mm:ss ص/م")
- `src/lib/excel-io.ts` — Excel export/import with Arabic+English headers, AM/PM and Excel-serial date parsing
- `src/lib/print-report.ts` — printable HTML report (now includes quantity column + 12-hour times)
