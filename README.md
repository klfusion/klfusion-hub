# KL Fusion Hub

Production-oriented multi-business SaaS rebuild of the original Hostinger + Supabase static prototype.

## Included modules

- Auth with Supabase SSR
- Business selection and creation
- Multi-business memberships and roles
- Multi-location inventory
- Dashboard snapshot
- Products with barcode and opening stock
- Categories
- Customers
- Suppliers
- Expenses
- POS checkout with tender modal
- Sales history and refunds
- Purchase orders and stock receiving
- Transfer orders between locations
- Invoices and quotations
- Portal sharing for quotes/invoices
- Recurring invoice templates
- Branded PDF generation for documents and receipts
- Reports summary
- Business settings
- Business admin with invitations and audit log
- Platform admin page

## Stack

- Next.js App Router
- React
- Tailwind CSS
- Supabase Auth + Postgres + RLS
- Server route handlers for privileged workflows
- pdf-lib for server-side PDF generation

## Quick start

1. Copy `.env.example` to `.env.local`
2. Add your Supabase project values
3. In Supabase SQL editor, run:

```sql
-- apply main schema
-- file: supabase/migrations/001_kl_fusion_hub.sql
```

4. Install and run:

```bash
npm install
npm run dev
```

## Required environment variables

```env
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
SUPABASE_SERVICE_ROLE_KEY=...
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

## Important production notes

- The app expects the SQL migration to be applied before first use.
- Public quote/invoice portal routes use the server-only service role key.
- Privileged workflows such as POS checkout, refunds, stock adjustments, purchase receiving, transfer completion and document save all run through RPC-backed route handlers.
- Recurring invoices are created by the SQL function `public.run_due_recurring_documents()`. Schedule it with Supabase cron or your preferred server scheduler.

## Suggested cron

Example frequency: every hour

```sql
select public.run_due_recurring_documents();
```

## File map

- `app/` - routes, layouts and API handlers
- `features/` - domain UI modules
- `components/` - shared UI
- `lib/` - Supabase helpers, PDF builders, formatting
- `supabase/migrations/` - schema, functions, RLS
- `legacy-reference/` - original uploaded static prototype

## Legacy reference

The original uploaded static prototype is included under `legacy-reference/` so the design and workflow source remain available during refinement.
