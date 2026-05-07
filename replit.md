# Workspace

## Overview

**PharmaCare** — A comprehensive Pharmacy Management Accounting System for Bangladeshi pharmacies.

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Project: PharmaCare

### Design
- Primary color: `#2BB673` (green)
- Sidebar: `#0A2540` (navy)
- Font: Inter
- Currency: Bangladeshi Taka (৳)
- Dark/light mode toggle supported

### Artifacts
1. **`artifacts/api-server`** — Express 5 REST API, Drizzle ORM + PostgreSQL
2. **`artifacts/pharmacy-app`** — React + Vite web frontend (serves at `/`)

### Features Implemented
- **Dashboard**: KPI cards, revenue/profit chart, low stock & expiry alerts, top medicines, quick actions
- **POS / Sales**: Cart-based point of sale with medicine search, VAT (7.5%), multiple payment methods (Cash/bKash/Nagad/Card), invoice printing
- **Inventory**: Medicine list with stock, pricing, expiry status; add/edit/delete medicines
- **Purchases**: Purchase invoices from suppliers, items tracking
- **Suppliers**: Full CRUD, contact info
- **Customers**: Full CRUD, contact info
- **Accounting**: Income/expense transactions, daily cashbook tab, P&L summary
- **Reports**: Sales report with chart, stock status report, expiry report
- **Users**: Staff accounts with roles (admin/manager/salesman), active status
- **Settings**: Pharmacy profile, VAT rate, currency, timezone settings

### Backend Routes (`artifacts/api-server/src/routes/`)
- `dashboard.ts` — summary, revenue chart, top medicines, alerts
- `medicines.ts` — CRUD + search/filter
- `sales.ts` — create sale (auto-deducts stock, creates accounting entry), list sales
- `purchases.ts` — CRUD purchase invoices (auto-increments stock)
- `suppliers.ts` — CRUD
- `customers.ts` — CRUD
- `accounting.ts` — transactions CRUD, cashbook, P&L
- `reports.ts` — sales report, stock report, expiry report
- `users.ts` — CRUD with password hashing

### DB Schema (`lib/db/src/schema/index.ts`)
Tables: `suppliers`, `medicines`, `customers`, `sales`, `sale_items`, `purchases`, `purchase_items`, `transactions`, `users`

### Seed Data (already loaded)
- 3 suppliers (Square Pharma, Beximco, ACI Healthcare)
- 3 customers
- 8 medicines (including low-stock and expired items for testing alerts)
- 3 sample sales
- 4 accounting transactions (rent, salary, utilities, income)
- 3 users (admin, manager, salesman)

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
