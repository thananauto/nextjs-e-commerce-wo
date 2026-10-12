# E-commerce Testing Application

A React + Vite + TypeScript e-commerce demo app — product catalog, shopping cart, authentication, checkout, order history, and an admin dashboard. It's built as a realistic client-side sandbox for practicing manual and automated (Playwright) testing. Despite the repository name, this is **not** a Next.js app — it's a Vite single-page application.

## Features

- **Product catalog** — browsable/searchable product grid with category filtering and detail views
- **Shopping cart** — add/remove items, update quantities, tax/shipping totals
- **Authentication** — login with role-based access (`admin` / `customer`), test accounts provided
- **Checkout & orders** — place an order from the cart, view order history, order confirmation page
- **Admin dashboard** — view all orders, inventory, and user overview (admin role only)
- **API testing page** — exercise the simulated backend's endpoints directly from the UI
- **WebMCP tools** — key flows (login, search, checkout) are also exposed as [Chrome WebMCP declarative](https://developer.chrome.com/docs/ai/webmcp/declarative-api) tools, so they can be driven by an AI agent in addition to a human user

## Architecture

There is no real server — all backend behavior is simulated client-side in-memory:

- `src/lib/api-backend.ts` — an in-memory fake REST backend (products, users, orders, cart, sessions), persisted via a `spark.kv` key-value store
- `src/lib/api-client.ts` — the `api` client components use to talk to the backend (`api.products.getAll()`, `api.cart.add()`, etc.)
- `src/lib/data.ts` — seed data and helpers used to initialize the backend
- `src/App.tsx` — manual client-side page routing (no router library)
- `src/components/ui/` — a shadcn/ui component set built on Radix primitives

See `CLAUDE.md` for a full architecture breakdown and `API_DOCS.md` for the complete simulated API reference.

## Getting Started

```bash
npm install --ignore-scripts   # see note below
npm run dev                    # starts dev server at http://localhost:5173/
```

**Test accounts** (see `API_DOCS.md`):

| Email | Password | Role |
|-------|----------|------|
| `admin@test.com` | `admin123` | Admin |
| `user@test.com` | `user123` | Customer |

### Other commands

```bash
npm run build                  # tsc -b --noCheck && vite build
npm run preview                # preview the production build
npm run test:e2e               # run the full Playwright suite
npm run test:e2e:ui            # Playwright UI mode
npm run test:e2e:browser       # UI flow tests only (tests/e2e/browser.spec.ts)
npm run test:e2e:api           # API flow tests only (tests/e2e/api.spec.ts)
```

**Note**: use `npm install --ignore-scripts` instead of a plain `npm install` — the `postinstall` Playwright browser download can fail/hang in restricted-network environments. Install browsers separately with `npx playwright install --with-deps` if you need to run the E2E suite.

## Documentation

- `CLAUDE.md` — architecture notes and guidance for working in this codebase
- `API_DOCS.md` — full simulated API reference (endpoints, response shapes, test accounts)
- `PRD.md` — product requirements and feature intent
- `SECURITY.md` — security policy

## Origin

This repository is a fork of [`nadvolod/nextjs-e-commerce-wo`](https://github.com/nadvolod/nextjs-e-commerce-wo), originally built as the main project for Nikolay Advolodkin's "AI For Good" workshop. See the `workshop/` directory for the original workshop materials.

## License

Licensed under the [MIT License](./LICENSE).
