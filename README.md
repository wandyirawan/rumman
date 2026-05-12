# Pomegranate Ecosystem 🍎

**The "Order What You Need" ERP.**

Odoo tries to be everything for everyone. We don't. Pomegranate is a modular ecosystem where you pick *only* the services your business needs. No bloat, no plugins, no $20/month "extra features" you never use.

> "Why buy a whole pizza when you're only hungry for a slice?"

---

## The Problem with "All-in-One" ERPs

| The Odoo Way | The Pomegranate Way |
| :--- | :--- |
| **Monolithic:** Install everything, hide what you don't use. | **Modular:** Install *only* what you need. |
| **Heavy:** Needs 2GB+ RAM just to load the dashboard. | **Light:** Runs on a $5 VPS (512MB RAM is enough). |
| **Plugin Hell:** Need a feature? Buy a plugin. Conflict? Good luck. | **Native:** Features are built-in. No plugins. No conflicts. |
| **Legacy Frontend:** jQuery/Owl. Feels like 2010. | **Modern:** HTMX + Alpine.js. Snappy, fast, clean. |
| **One Language:** Python (for everything). | **Right Tool:** Rust (Speed), Go (Simplicity), Elixir (Concurrency). |

---

## What We've Built (The "Ala Carte" Menu)

### 1. Mangosteen (Identity Core) 🥭
*The gatekeeper. Handles users, roles, and auth for everything.*
- **Need it?** Yes, if you have users.
- **Tech:** Go (15MB RAM idle).
- **Status:** ✅ **Ready**
- **Repo:** https://github.com/wandyirawan/mangosteen

### 2. Granate (CMS & Content) 🍎
*Your landing pages, SEO, and product details. Fast.*
- **Need it?** Yes, if you have a public face.
- **Tech:** Rust (8MB idle). Serves content at native speed.
- **Status:** ✅ **Ready**
- **Repo:** https://github.com/wandyirawan/granate

### 3. Pome (The Dashboard) 🍊
*One frontend to rule them all. Storefront + Admin.*
- **Need it?** Yes, you need a UI.
- **Tech:** Bun + HTMX. No React bloat.
- **Status:** ✅ **Ready**
- **Repo:** https://github.com/wandyirawan/pome

### 4. Salak (Inventory) 🐍
*Stock management that never loses count. Audit-ready.*
- **Need it?** Yes, if you have products.
- **Tech:** Python + Granian (Rust server). DB Triggers for ACID.
- **Status:** ✅ **Ready**
- **Repo:** https://github.com/wandyirawan/salak

---

## What's Cooking? (The Roadmap)

Don't order it if you don't need it.

### 🛒 Ecommerce (Pomelo)
*Online store for thousands of concurrent buyers.*
- **Need it?** If you sell online.
- **Tech:** Elixir + Phoenix (The concurrency king).
- **Status:** 🔜 Planning

### 👥 HR App
*Manage your team, leaves, and payroll.*
- **Need it?** If you have employees.
- **Tech:** Go (Simple, fast, reliable).
- **Status:** 🔜 Planning

### 📊 CRM
*Track leads and sales pipelines.*
- **Need it?** If you have a sales team.
- **Tech:** Go.
- **Status:** 🔜 Planning

### 💰 Accounting
*Ledger, taxes, and financial reports.*
- **Need it?** If you want to stay legal.
- **Tech:** Python (Rich finance libs).
- **Status:** 🔜 Planning

---

## Architecture: Simple by Design

```
[User] → Pome (UI) → [JWT from Mangosteen]
                      ↓
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
    Granate        Salak        [Future Services]
    (Content)     (Stock)      (Only if you need 'em)
```

---

## Why "Fruit Salad"?

Because every fruit has its own taste (purpose).
- **Mangosteen:** Hard shell, sweet inside (Security).
- **Granate:** Hard seeds, juicy fruit (Content/Speed).
- **Salak:** Snake skin, crisp inside (Data/Inventory).

We don't force-feed you a banana if you wanted an apple.

---

## Get Started (in 3 steps)

1. **Clone the service you need.**
   ```bash
   git clone https://github.com/wandyirawan/salak.git
   ```
2. **Run it.**
   ```bash
   make dev
   ```
3. **Done.** Runs on port 8000.

---

**Pomegranate Ecosystem** — *ERP for those who hate ERP bloat.*
