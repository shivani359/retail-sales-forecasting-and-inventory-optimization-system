# Retail Sales Forecasting & Inventory Optimization

A Python portfolio project that generates realistic synthetic retail sales,
evaluates a demand forecast, and demonstrates inventory reorder decisions in a
Streamlit dashboard.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- The retail dashboard needs no secrets or database; `DATABASE_URL` is only
  required by the unused starter API if you choose to run it.
- Retail dashboard workflow: `Retail Forecasting Dashboard` (Streamlit on port 3000)
- Local Python commands and setup: `retail-sales-forecasting-inventory-optimization/README.md`
- Python tests: `cd retail-sales-forecasting-inventory-optimization && python -m unittest discover -s tests -v`

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)
- Retail portfolio app: Python 3.11+, Streamlit, pandas, NumPy, scikit-learn,
  matplotlib, seaborn

## Where things live

- `retail-sales-forecasting-inventory-optimization/` — the complete
  self-contained portfolio project, README, scripts, source modules, tests,
  synthetic dataset, generated charts, and reports.
- `artifacts/api-server/` and `lib/` — the starter workspace's shared API and
  TypeScript libraries; the retail dashboard does not depend on them.
- `replit.md` — project run commands and durable implementation notes.

## Architecture decisions

- Synthetic data is deterministic because the project must be reproducible
  without access to a retailer's private systems.
- The forecast target is fulfilled `units_sold`; latent
  `simulated_demand` is never a model feature.
- Backtesting uses a chronological holdout and recursively feeds predictions
  forward; a seasonal-naive baseline is reported alongside the Random Forest.
- The selected SKU's dashboard reorder row uses its forecast mean; other queue
  rows use recent demand averages. The simulation-only latent demand provides
  variability for safety stock.

## Product

- Interactive sales and stockout overview by store and product.
- Random Forest demand forecast, recursive holdout comparison, and downloadable
  forecast CSV.
- Safety stock, reorder point, days of cover, reorder queue, and CSV export.
- Beginner-friendly setup, simulation, testing, GitHub, and interview guide.

## User preferences

- Keep the project beginner-friendly, practical, reproducible, and suitable as
  GitHub proof of work; clearly label all generated outcomes as synthetic.

## Gotchas

- Run Python scripts from inside
  `retail-sales-forecasting-inventory-optimization/`.
- The dashboard workflow uses port 3000 so it does not conflict with the shared
  API server on port 5000.
- The evaluation metrics are from synthetic data only; do not present them as
  measured retailer performance.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
