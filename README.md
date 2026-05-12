# Salad Buah (Pomegranate Ecosystem)

Lightweight ERP ecosystem inspired by fruit names. Built for small-to-medium businesses that want Odoo-like functionality without the bloat.

**Philosophy:** Modular microservices, each doing one thing well. Runs on affordable VPS (starting 85k IDR = 2 vCPU, 2GB RAM).

---

## What We've Built (Already Running)

### 1. Mangosteen (Identity Provider)
- **Tech:** Go + Fiber + SQLite
- **Function:** Authentication & Authorization (IAM) for ALL services
- **Status:** ✅ Production
- **Repo:** https://github.com/wandyirawan/mangosteen
- **Port:** 4000
- **Key Feature:** JWKS endpoint for JWT verification (`/api/.well-known/jwks.json`)

### 2. Granate (CMS & Content)
- **Tech:** Rust + Axum + PostgreSQL
- **Function:** Content Management System, SEO, Landing Pages, Product Details
- **Status:** ✅ Production
- **Repo:** https://github.com/wandyirawan/granate
- **Port:** 3000
- **Key Feature:** Integrates with Mangosteen for auth, lightweight (8MB idle RAM)

### 3. Pome (Frontend Head)
- **Tech:** Bun + Elysia + HTMX + Alpine.js + Pico CSS
- **Function:** Universal dashboard & storefront
- **Status:** ✅ Production
- **Repo:** https://github.com/wandyirawan/pome
- **Port:** 4021
- **Key Feature:** Lightweight interactive UI without React/Vue bloat

### 4. Salak (Inventory Service)
- **Tech:** Python + FastAPI + Granian (Rust server) + PostgreSQL
- **Function:** Stock management with ACID compliance
- **Status:** ✅ Production (Step 1-5 done)
- **Repo:** https://github.com/wandyirawan/salak
- **Port:** 8000
- **Key Feature:** Database trigger auto-updates `real_qty` from `delta_qty` (history)

---

## Planned Milestones

### Milestone 1: Ecommerce Service
- **Tech:** Elixir + Phoenix
- **Function:** Online storefront, cart, checkout, payment gateway integration
- **Why Elixir:** Handles thousands of concurrent users (flash sales) without crashing
- **Integration:** Calls Salak (inventory check), uses Mangosteen (auth)
- **Status:** 🔜 Planning

### Milestone 2: HR Application
- **Tech:** Go + Fiber (similar to Mangosteen)
- **Function:** Employee management, leave requests, payroll, attendance
- **Key Feature:** Uses Salak for company asset tracking
- **Status:** 🔜 Planning

### Milestone 3: CRM Service
- **Tech:** Go + Fiber
- **Function:** Customer data, sales pipeline, lead management, follow-up tracking
- **Integration:** Receives data from Ecommerce service
- **Status:** 🔜 Planning

### Milestone 4: Accounting Service
- **Tech:** Python + FastAPI + Granian
- **Function:** Ledger, invoicing, tax calculation, financial reports
- **Why Python:** Rich ecosystem for financial libraries
- **Integration:** Reads from Salak (inventory valuation), Ecommerce (sales), HR (payroll)
- **Status:** 🔜 Planning

---

## Architecture Diagram

```
[All Users] → Mangosteen (Auth/SSO)
                    ↓
        ┌───────────┬───────────┬───────────┐
        ↓           ↓           ↓           ↓
    Pome (UI)   Granate     Salak      [Future Services]
    (Frontend)  (CMS)    (Inventory)  (Ecommerce, HR, CRM, etc.)
                    ↓           ↓
                [Public]   [Internal/External]
```

---

## Design Principles

1. **Lightweight First:** Every service must run on 85k IDR VPS (2 vCPU, 2GB RAM)
2. **Modular:** Each service is independent, can be deployed separately
3. **No PHP:** Avoiding WordPress/WooCommerce bloat
4. **Right Tool for Job:**
   - Rust: Speed & safety (CMS)
   - Go: Simple & fast (Auth, HR)
   - Python: Data & finance (Inventory, Accounting)
   - Elixir: Concurrency (Ecommerce)
   - Bun: Fast frontend (UI)

---

## Getting Started

Each service has its own repo with:
- `README.md` (setup instructions)
- `Makefile` (for `make dev` one-command startup)
- Docker Compose (for database/dependencies)
- Step-by-step commits (milestone tracking)

---

**Part of Pomegranate Ecosystem** 🍎

"Ecommerce for small businesses that don't want WooCommerce's bloat. Runs on a $5 VPS, no plugins, no PHP."
