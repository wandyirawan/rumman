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
      └─────────────┘ └──────┘ └─────────────┘
      ┌─────────────┐ ┌──────┐
      │   Kelapa    │ │ Pome │
      │(Elixir/Phoen│ │(Bun) │
      │  E-commerce │ │BO UI │
      └─────────────┘ └──────┘
```

Each service is independently deployable, owns its own database, and communicates via REST APIs authenticated through Mangosteen (universal IAM).

---

## Services

| Service | Language | Domain | Status |
| :--- | :--- | :--- | :--- |
| **Mangosteen** | Go (Fiber) | Authentication & IAM | ✅ Ready |
| **Salak** | Python (FastAPI + Granian) | Product Catalog & Inventory | ✅ Ready |
| **Granate** | Rust (Axum) | CMS, SEO, Object Storage (Minio) | ✅ Ready |
| **Pome** | TypeScript (Bun + Elysia + HTMX) | Backoffice Dashboard | ✅ Ready |
| **Duwet** | Rust (Ratatui) | Warehouse TUI Client | ✅ Ready |
| **Kelapa** | Elixir (Phoenix + Elm) | E-commerce Storefront | 🔜 In Progress |

---

## Technical Highlights

- **Universal IAM** — Single JWT-based auth across all services (Mangosteen)
- **ACID Inventory** — Postgres triggers for stock consistency, sync-first design
- **Full-Text Search** — PostgreSQL ILIKE + GIN trigram indexes (pg_trgm)
- **Zero ORM** — Raw SQL with migration-based schema management
- **Zero-Warning Rust** — Granate compiles clean with strict lints
- **Lightweight** — Go services idle at ~15MB RAM, Rust at ~8MB

---

## Design Philosophy

**Sync over async.** Data consistency before performance theater.

**Raw SQL over ORM.** No magic queries. No N+1 surprises.

**API-first.** Every service exposes REST APIs. Build your own frontend — ours (Pome) is just a reference implementation.

**Modular, not monolithic.** Run only what you need. Minimum stack: Mangosteen + Salak = auth + inventory.

---

## Repositories

| Service | Repository |
| :--- | :--- |
| Mangosteen (Auth) | [github.com/wandyirawan/mangosteen](https://github.com/wandyirawan/mangosteen) |
| Salak (Inventory) | [github.com/wandyirawan/salak](https://github.com/wandyirawan/salak) |
| Granate (CMS) | [github.com/wandyirawan/granate](https://github.com/wandyirawan/granate) |
| Pome (Backoffice) | [github.com/wandyirawan/pome](https://github.com/wandyirawan/pome) |
| Duwet (Warehouse TUI) | [github.com/wandyirawan/duwet](https://github.com/wandyirawan/duwet) |
| Kelapa (E-commerce) | [github.com/wandyirawan/kelapa](https://github.com/wandyirawan/kelapa) |

---

## Quick Start

```bash
# Minimum viable stack: auth + inventory
git clone https://github.com/wandyirawan/mangosteen.git
git clone https://github.com/wandyirawan/salak.git
cd mangosteen && make dev &
cd salak && make dev &
# Build your own frontend, or use Pome as reference
git clone https://github.com/wandyirawan/pome.git
```

---

**Rumman** — *رُمَّان. The fruit. The platform. Pick what you need.*
