# Rumman (رُمَّان) — Polyglot Modular Enterprise Platform

**API-first, polyglot microservices. Pick only what you need.**

Rumman is a modular enterprise platform built as independent polyglot services — each service owns its database, its language, and its domain. No monolith. No vendor lock-in. No forced frontend.

> "Don't like our frontend? Replace it. The APIs are open."

Internally, services are named after fruits (hence "Pomegranate Ecosystem"). Externally: **Rumman**.

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│              [Your Frontend]                     │
│         React / Vue / Svelte / Mobile            │
└────────────┬────────────┬────────────┬───────────┘
             │            │            │
      ┌──────▼──────┐ ┌──▼───┐ ┌──────▼──────┐
      │ Mangosteen  │ │ Salak│ │   Granate   │
      │ (Go/Fiber)  │ │(Py)  │ │ (Rust/Axum) │
      │   Auth/IAM  │ │Inv.  │ │    CMS      │
      └─────────────┘ └──┬───┘ └─────────────┘
                         │
      ┌─────────────┐ ┌──▼───┐ ┌─────────────┐
      │   Orange    │ │ Lime │ │   Kelapa    │
      │ (Python)    │ │(Py)  │ │(Elixir/Phoen│
      │   Sales     │ │Acc.  │ │  E-commerce │
      └─────────────┘ └──────┘ └─────────────┘
             │            │
             └─────┬──────┘
              ┌────▼────┐
              │  Lemon  │  ← Orchestrator
              │  (Py)   │     `lemon dev`
              └─────────┘
```

Each service is independently deployable, owns its own database, and communicates via REST APIs authenticated through Mangosteen (universal IAM).

---

## Services

| Service | Language | Domain | Port | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Mangosteen** | Go (Fiber) | Authentication & IAM | 4000 | ✅ Ready |
| **Salak** | Python (FastAPI + Granian) | Product Catalog & Inventory | 8000 | ✅ Ready |
| **Orange** | Python (FastAPI + Granian) | Sales Orders, Invoicing | 8001 | 🚧 Active |
| **Lime** | Python (FastAPI + Granian) | Accounting & Ledger | 8003 | 🚧 Active |
| **Granate** | Rust (Axum) | CMS, SEO, Object Storage (Minio) | 8002 | ✅ Ready |
| **Pome** | TypeScript (Bun + Elysia + HTMX) | Backoffice Dashboard | 4021 | ✅ Ready |
| **Duwet** | Rust (Ratatui) | Warehouse TUI Client | — | ✅ Ready |
| **Lemon** | Python (CLI) | Service Orchestrator | — | 🚧 Active |
| **Kelapa** | Elixir (Phoenix + Elm) | E-commerce Storefront | TBD | 🔜 In Progress |

### Deployment Tiers

```
Minimal:     Mangosteen + Salak                     (auth + inventory)
Standard:    Mangosteen + Salak + Orange            (+ sales tracking)
Complete:    Mangosteen + Salak + Orange + Lime     (+ accounting)
Frontend:    + Pome                                  (backoffice dashboard)
E-commerce:  + Kelapa                                (storefront)
```

---

## Domain Boundaries

### Inventory (Salak)
- Single source of truth: stock qty, COGS, stock movements
- Does NOT know about customers, selling prices, or money
- Database triggers for ACID stock consistency

### Sales (Orange)
- Order lifecycle: pending → confirmed → invoiced → paid → delivered
- Multi-channel: POS, ecommerce, B2B
- Delegates stock reservation to Salak
- Sends invoices to Lime (Accounting)
- Does NOT create accounting journals — delegates to Lime

### Accounting (Lime)
- Double-entry bookkeeping (debit = credit)
- Pre-configured Chart of Accounts for Indonesian UMKM
- Revenue + PPh Final (0.5%) auto-journaling
- Profit & Loss reports
- Idempotent — won't double-book the same invoice

### Pricing Boundary
- **Salak stores COGS** — harga pokok perolehan
- **Orange stores selling prices** — harga jual, per-channel overrides, diskon
- Sales validates selling_price >= COGS (block by default, override for clearance)

### Corrections
All append-only. Never DELETE transactions:
- Stock adjustments: `stock_movements` with type=adjustment
- Sales corrections: reversal orders, not row deletion
- Accounting: adjustment journal entries

---

## Technical Highlights

- **Universal IAM** — Single JWT-based auth across all services (Mangosteen)
- **ACID Inventory** — Postgres triggers for stock consistency, sync-first design
- **Full-Text Search** — PostgreSQL ILIKE + GIN trigram indexes (pg_trgm)
- **Zero ORM** — Raw SQL with migration-based schema management
- **Zero-Warning Rust** — Granate compiles clean with strict lints
- **Lightweight** — Go services idle at ~15MB RAM, Rust at ~8MB, Python/Granian at ~40MB
- **Server Kentang** — Runs on VPS 1GB RAM or Raspberry Pi. No Kafka/RabbitMQ needed
- **Orchestration** — `lemon dev` starts entire core stack with one command

---

## Design Philosophy

**Sync over async.** Data consistency before performance theater.

**Raw SQL over ORM.** No magic queries. No N+1 surprises.

**API-first.** Every service exposes REST APIs. Build your own frontend — ours (Pome) is just a reference implementation.

**Modular, not monolithic.** Run only what you need. Minimum stack: Mangosteen + Salak = auth + inventory.

**Append-only.** Corrections via adjustment entries, never deletes.

---

## Repositories

| Service | Repository |
| :--- | :--- |
| Mangosteen (Auth) | [github.com/wandyirawan/mangosteen](https://github.com/wandyirawan/mangosteen) |
| Salak (Inventory) | [github.com/wandyirawan/salak](https://github.com/wandyirawan/salak) |
| Orange (Sales) | [github.com/wandyirawan/orange](https://github.com/wandyirawan/orange) |
| Lime (Accounting) | [github.com/wandyirawan/lime](https://github.com/wandyirawan/lime) |
| Lemon (Orchestrator) | [github.com/wandyirawan/lemon](https://github.com/wandyirawan/lemon) |
| Granate (CMS) | [github.com/wandyirawan/granate](https://github.com/wandyirawan/granate) |
| Pome (Backoffice) | [github.com/wandyirawan/pome](https://github.com/wandyirawan/pome) |
| Duwet (Warehouse TUI) | [github.com/wandyirawan/duwet](https://github.com/wandyirawan/duwet) |
| Kelapa (E-commerce) | [github.com/wandyirawan/kelapa](https://github.com/wandyirawan/kelapa) |

---

## Quick Start

```bash
# Clone orchestrator (or clone individual services)
git clone https://github.com/wandyirawan/lemon.git
cd lemon
uv sync

# Start core dev stack (auth + inventory + sales + accounting)
uv run lemon dev

# Check status
uv run lemon status
```

Or the manual way:

```bash
# Minimum viable stack: auth + inventory
git clone https://github.com/wandyirawan/mangosteen.git
git clone https://github.com/wandyirawan/salak.git
cd mangosteen && make dev &
cd salak && make dev &
```

---

## Project Milestones

### Phase 1: Foundation ✅
- [x] Mangosteen — JWT auth (Go/Fiber)
- [x] Salak — Inventory + stock triggers (Python/Granian)
- [x] Granate — CMS + object storage (Rust/Axum)
- [x] Pome — Backoffice dashboard (Bun/HTMX)
- [x] Duwet — Warehouse TUI (Rust/Ratatui)

### Phase 2: Commerce 🚧
- [x] Orange — Sales order lifecycle, invoicing
- [x] Lime — Double-entry accounting, P&L
- [x] Lemon — Service orchestrator CLI
- [ ] Orange ↔ Salak stock reservation
- [ ] Orange ↔ Lime invoice flow end-to-end
- [ ] Pricing rules (COGS validation)

### Phase 3: Storefront 🔜
- [ ] Kelapa — E-commerce storefront (Elixir/Phoenix + Elm)
- [ ] Multi-channel: POS, B2B, marketplace
- [ ] Payment gateway integration (QRIS, e-wallets)

### Phase 4: Production 🔜
- [ ] Integration tests across all services
- [ ] CI/CD pipeline
- [ ] Production deployment guide (Docker Compose)
- [ ] Monitoring & health dashboards

---

**Rumman** — *رُمَّان. The fruit. The platform. Pick what you need.*
