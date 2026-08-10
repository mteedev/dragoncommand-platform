<div align="center">

![DragonCommand](https://raw.githubusercontent.com/mteedev/dragoncommand-platform/main/assets/DragonCommand_Logo_Poster_intro2.jpg)

<br />

# DragonCommand

### The OpenSimulator Grid Command Platform

**Full Stack. Modern. Powerful. No PHP. No Limits.**

[![Status](https://img.shields.io/badge/status-in%20development-red?style=for-the-badge&logo=dragon&logoColor=white)](https://msaxiom.com)
[![Stack](https://img.shields.io/badge/stack-Next.js%2016%20%2B%20TypeScript-black?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![License](https://img.shields.io/badge/license-proprietary-gold?style=for-the-badge)](LICENSE)
[![Demo](https://img.shields.io/badge/live%20demo-msaxiom.com-darkred?style=for-the-badge)](https://www.msaxiom.com)

---

*Command Your Grid. Empower Your Community.*

</div>

---

## What is DragonCommand?

DragonCommand is a **full-stack OpenSimulator grid management platform** built to replace the aging PHP stack that the OpenSimulator community has relied on for decades — WordPress, w4os, ORBIT, WooCommerce — with a single, modern, unified platform purpose-built for grid operators and their residents.

No more duct-taped plugins. No more WordPress security patches at 2am. No more six different dashboards to manage one grid.

**One platform. Total control.**

---

## The Problem

Every serious OpenSimulator grid today cobbles together some combination of:

- **WordPress + w4os** for resident registration and profiles
- **ORBIT or similar** for admin management
- **WooCommerce** for a marketplace
- **Custom PHP scripts** for everything else
- **Multiple databases** that don't talk to each other cleanly
- **Zero real-time anything**

This stack was never designed to work together. It just... accumulated. Grid owners spend more time maintaining infrastructure than building communities.

---

## The Solution

DragonCommand replaces the entire stack with a single, cohesive platform:

```
┌─────────────────────────────────────────────────────────────┐
│                      DragonCommand                          │
├────────────────────────┬────────────────────────────────────┤
│   PUBLIC GRID SITE     │         RESIDENT PORTAL            │
│  grid.example.com      │    grid.example.com/me             │
│                        │                                    │
│  • Hero landing page   │  • Profile (Info/Friends/Picks)   │
│  • Events calendar     │  • Inventory tree (IAR export)    │
│  • Marketplace browse  │  • Currency balance + history     │
│  • Registration funnel │  • Region management (OAR/restart)│
│  • How to connect      │  • Friends list                   │
├────────────────────────┴────────────────────────────────────┤
│                    ADMIN PANEL                              │
│               panel.grid.example.com                       │
│                                                            │
│  • User management + Dragon Rank system                    │
│  • Region management (ORBIT replacement)                   │
│  • Ghost Hunter (automated account cleanup)                │
│  • Grid configuration + branding                           │
│  • Audit log                                               │
│  • Add-On module management                                │
├────────────────────────────────────────────────────────────┤
│              BIDIRECTIONAL GRID BRIDGE                     │
│                                                            │
│         LSL → API → WebSocket → UI                        │
│         Grid Events → Web → Back to Grid                  │
│                                                            │
│         Real-time. Secure. No polling hacks.              │
└────────────────────────────────────────────────────────────┘
```

---

## Dragon Rank System

DragonCommand replaces the traditional WordPress role system with a purpose-built rank hierarchy designed for OpenSimulator grids:

| Rank | Level | Access |
|------|-------|--------|
| 🥚 Hatchling | 0 | Web account created, no avatar yet |
| 🐣 Fledgling | 1 | Avatar created, full grid access + region panel |
| 🐲 Wyvern | 2 | Junior staff |
| 🐉 Drake | 3 | Senior staff — full user management |
| ⚔️ Ancient | 4 | Super Admin |
| 👑 DragonMaster | 5 | God mode — grid owner |

---

## Tech Stack

DragonCommand is built on a modern, type-safe, production-grade stack — chosen deliberately, not by accident:

| Layer | Technology | Why |
|-------|-----------|-----|
| **Framework** | Next.js 16+ / Vite 8 | Full-stack React, App Router, RSC |
| **Language** | TypeScript (strict) | Type safety throughout, no surprises |
| **Monorepo** | pnpm Workspaces + Turborepo | Scalable, fast, clean package boundaries |
| **Styling** | Tailwind v4 + shadcn/ui | Consistent, accessible, beautiful |
| **Data Fetching** | TanStack Query + TanStack Router | Real-time, caching, type-safe routing |
| **ORM** | Drizzle ORM | Type-safe, lightweight, PostgreSQL-first |
| **Auth** | better-auth | Modern auth — sessions, rate limiting, cross-subdomain |
| **Observability** | Sentry + Structured Logging | Know what's happening, always |
| **Build** | Turborepo | Monorepo build pipeline, incremental builds |

---

## Architecture

DragonCommand is designed for the real-world topology of a production OpenSimulator grid:

```
INTERNET
    │
    ├── grid.example.com      ← Public grid website + resident portal
    ├── panel.grid.example.com ← Admin panel (Drake+ rank required)
    │
    ▼
DragonCommand VPS (Next.js + PostgreSQL)
    │
    │  ← Tailscale mesh / secure tunnel →
    │
    ▼
Robust Server (MySQL/MariaDB)
    │
    ├── UserAccounts, auth, inventory
    ├── Regions, Parcels, Friends
    ├── GridUser (presence/online status)
    └── Economy tables
```

**Multi-tenant from day one.** Every table carries a `grid_id`. One DragonCommand installation can serve multiple grids — the foundation for the future SaaS tier.

---

## Two-Stage Account Architecture

One of DragonCommand's core design decisions: **web registration never touches your Robust database until the user actually creates an avatar.**

```
Stage 1 — Web Registration
  User signs up with email + password
  → Written to DragonCommand DB only
  → Robust DB: untouched
  → Status: Hatchling 🥚

Stage 2 — Avatar Creation
  User picks First Name + Last Name
  User picks appearance
  → UserAccounts, auth, inventory folders written to Robust DB
  → Status: Fledgling 🐣
```

Bot registrations, abandoned sign-ups, and ghost accounts cost a single row deletion — your Robust database stays clean by design.

---

## Add-On Modules

DragonCommand ships with a powerful core and an extensible module system. Grid operators can unlock additional capabilities:

| Module | Description | Type |
|--------|-------------|------|
| **Marketplace** | Vendor dashboard, storefronts, in-world delivery | Paid Add-On |
| **Events** | Public events calendar, GateCrashers integration | Add-On |
| **Land Sales** | Parcel listing, purchase flow, rental management | Add-On |
| **Partner System** | Affiliate/referral tracking for grid growth | Add-On |
| **Economy Dashboard** | Transaction history, balance management, reports | Add-On |

---

## Live Demo

DragonCommand is currently in active development, running live on the **MS Axiom Virtual Cruise Grid** — a 969-meter virtual cruise ship in the OpenSimulator metaverse.

| URL | Description |
|-----|-------------|
| [www.msaxiom.com](https://www.msaxiom.com) | Public grid website |
| [www.msaxiom.com/register](https://www.msaxiom.com/register) | Registration flow (currently closed) |
| [panel.msaxiom.com](https://panel.msaxiom.com) | Admin panel (login required) |

---

## Roadmap

### Phase 1 — The Egg ✅ (Complete)
- [x] Monorepo scaffold + all packages
- [x] PostgreSQL schema (12 tables)
- [x] OpenSim Robust DB bridge
- [x] better-auth (cross-subdomain sessions)
- [x] Public grid website
- [x] Resident portal shell (/me)
- [x] Admin panel with login + auth middleware
- [x] Systemd services + SSL

### Phase 2 — The Hatchling 🔄 (In Progress)
- [ ] Tailscale mesh (VPS ↔ Proxmox)
- [ ] Standalone → Grid Hypergrid conversion (MS Axiom)
- [ ] Live Robust DB wiring (profile, friends, inventory, regions)
- [ ] Avatar creation flow (Stage 2 → Robust DB write)
- [ ] Email verification (Postfix + DKIM)

### Phase 3 — The Fledgling 📋 (Planned)
- [ ] Full resident portal (inventory tree, region OAR/restart, friends)
- [ ] Admin user management + Ghost Hunter
- [ ] Dragon Rank management UI
- [ ] Grid configuration wizard
- [ ] Audit log viewer

### Phase 4 — The Drake 🗓️ (Future)
- [ ] Marketplace Add-On module
- [ ] Events Add-On module
- [ ] Multi-tenant SaaS tier
- [ ] White-label branding system
- [ ] LibreMetaverse .NET sidecar (gRPC bridge)

---

## For Grid Operators

DragonCommand is being built with the real-world OpenSimulator operator in mind:

- **No Docker required** — deploys as systemd services on any Ubuntu/Debian VPS
- **Self-hosted email** — Postfix + DKIM, no per-email charges
- **Works with your existing Robust DB** — no migration, no data loss
- **Grid-mode first** — designed around the Robust server architecture that powers grids like NeverWorld Grid
- **White-label ready** — every grid gets its own branding; the "Powered by DragonCommand" watermark stays

---

## Early Access

DragonCommand is not yet available for public installation. If you operate an OpenSimulator grid and want to be notified when early access opens:

**Watch this repository** to follow development progress.

For direct inquiries: open a [Discussion](https://github.com/mteedev/dragoncommand-platform/discussions) or reach out via the MS Axiom grid.

---

## About

DragonCommand is being built by **Mark Teegardin** (Gundahar Bravin in-world), Events Manager, Web Admin, and Developer at [NeverWorld Grid](https://neverworldgrid.com) — with 15+ years of virtual world development experience.

*Built by a grid operator, for grid operators.*

---

<div align="center">

**༺🐲༻**

*DragonCommand — Grid-Wide. Locked Down. Ready to Fly.*

**FULL STACK. MODERN. POWERFUL. NO PHP. NO LIMITS.**

</div>
