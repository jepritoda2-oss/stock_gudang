# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Contains a Dashboard Stok Gudang (Warehouse Stock Dashboard) web app.

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
- **Frontend**: React + Vite + TailwindCSS

## Artifacts

### stok-gudang (Dashboard Stok Gudang)
- **Preview path**: `/`
- **Type**: react-vite
- **Description**: Warehouse inventory management dashboard in Indonesian (Bahasa Indonesia)
- **Features**:
  - Category cards showing item count and total stock
  - Add/delete categories with custom icon and color
  - Add items with stock-in tracking, entry date, expiry date
  - Stock-in and Stock-out adjustments with quantity and notes
  - Transaction history per item
  - Search and filter items by name and status
  - Status badges: STOK AMAN / STOK SEDANG / STOK KRITIS / STOK HABIS
  - Export to CSV (per category or all)
  - Fully mobile responsive
  - No login required — accessible from any device

### api-server (API Server)
- **Preview path**: `/api`
- **Type**: Express API
- **Routes**: /api/categories, /api/items, /api/transactions, /api/export

## Database Schema

- `categories` — name, icon, color
- `items` — categoryId, name, stockIn, stockOut, entryDate, expiryDate
- `transactions` — itemId, type (in/out), quantity, note

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## Notes
- After codegen, fix `lib/api-zod/src/index.ts` to only export from `./generated/api` (not types) to avoid duplicate export conflicts
