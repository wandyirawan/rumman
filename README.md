# Salad Buah (Fruit Salad ERP) 🍎🍊🍇

**The Modular ERP. You bring the frontend, we bring the APIs.**

Stop forcing your business into a monolithic CMS. Salad Buah provides the backend services (Auth, Inventory, CMS). Want a React dashboard? Go ahead. Prefer Vue? Sure. Our default "Head" (Pome) is just an example built with Bun + HTMX.

> "Don't like our frontend? Replace it. The APIs are open."

---

## What's in the Salad?

Every service is named after a fruit. Pick what you need:

| Fruit | Service | Function |
| :--- | :--- | :--- |
| **Mangosteen** 🥭 | Identity Provider | Auth for ALL users |
| **Granate** 🍎 | CMS & Content | SEO, Landing Pages |
| **Salak** 🐍 | Inventory | Stock management |
| **Pome** 🍊 | Reference Frontend | Example UI (Bun+HTMX) |
| **Kelapa** 🥥 | Ecommerce | Online store (Planned) |
| **Mango** 🥭 | HR App | Employee management (Planned) |
| **Lemon** 🍋 | Accounting | Finance & tax (Planned) |
| **Berry** 🍇 | CRM | Customer relations (Planned) |

---

## Minimum Stack (What you *actually* need)

Most businesses don't need a CMS. They need **Users** and **Stock**.

| Need | Service | Status |
| :--- | :--- | :--- |
| **Login & Users** | **Mangosteen** (Go) | ✅ Ready |
| **Stock & Inventory** | **Salak** (Python) | ✅ Ready |
| **Content/SEO (Optional)** | Granate (Rust) | ✅ Ready |
| **Online Store (Optional)** | Kelapa (Elixir) | 🔜 Planning |

**TL;DR:** Run Mangosteen + Salak. You're good to go.

---

## The "Bring Your Own Frontend" Philosophy

### Pome (Our Example)
We built **Pome** (Bun + Elysia + HTMX) to show you how easy it is to consume our APIs.
- **Is it mandatory?** No.
- **Can I fork it?** Yes, MIT License.
- **Can I use React/Next.js?** **YES.**

### How it works
```
[Your Custom Frontend (React/Vue/Svelte)]
          ↓ (JWT Token from Mangosteen)
[Mangosteen (Auth)] -----> [Salak (Inventory)]
                           [Granate (CMS)] <--- (Optional)
```

---

## What We've Built (The Backend)

### 1. Mangosteen (Identity Provider) 🥭
*The Gatekeeper. Handles Auth for everything.*
- **Tech:** Go + Fiber (15MB RAM idle).
- **Repo:** https://github.com/wandyirawan/mangosteen
- **Why:** Lightweight Identity Provider. No bloat.

### 2. Salak (Inventory) 🐍
*Audit-ready stock management.*
- **Tech:** Python + Granian (Rust Server).
- **Repo:** https://github.com/wandyirawan/salak
- **Why:** ACID-compliant stock updates via Postgres Triggers.

### 3. Granate (CMS & Content) 🍎
*Landing pages, SEO, Product Details.*
- **Tech:** Rust + Axum (8MB RAM idle).
- **Repo:** https://github.com/wandyirawan/granate
- **Why:** Speed. If you don't need content, don't run it.

### 4. Pome (Reference Frontend) 🍊
*The example client. Built with Bun + HTMX.*
- **Tech:** Bun + Elysia + HTMX + Alpine.js.
- **Repo:** https://github.com/wandyirawan/pome
- **Why:** To prove how simple it is to talk to our APIs.

---

## Roadmap (The "Odoo" Features, but Modular)

### 🛒 Ecommerce (Kelapa)
*Flash sales without crashing.*
- **Tech:** Elixir + Phoenix (Concurrency King).
- **Status:** 🔜 Planning

### 👥 HR App
*Manage your team.*
- **Tech:** Go + Fiber.
- **Status:** 🔜 Planning

### 📊 CRM
*Sales pipelines.*
- **Tech:** Go + Fiber.
- **Status:** 🔜 Planning

### 💰 Accounting
*Ledger & Taxes.*
- **Tech:** Python + Granian.
- **Status:** 🔜 Planning

---

## Why not Odoo?

| Feature | Odoo | **Salad Buah** |
| :--- | :--- | :--- |
| **Architecture** | Monolith (Force everything) | **Modular** (Pick what you need) |
| **Frontend** | jQuery/Owl (Legacy) | **BYOF** (Bring Your Own Frontend) |
| **Resource** | 2GB RAM (Heavy) | **80MB Total** (Light) |
| **Customization** | Python Inheritance | **API-First** (Any language) |
| **Naming** | Just "Apps" | **Fruit Names** (Fun & Memorable) |

---

## Get Started (The Minimal Way)

1. **Clone Auth:** `git clone https://github.com/wandyirawan/mangosteen.git`
2. **Clone Inventory:** `git clone https://github.com/wandyirawan/salak.git`
3. **Run:** `make dev` on both.
4. **Build your own Frontend** (or use Pome as a starter).

---

**Salad Buah** — *Pick the fruits you need. Skip the rest.*
