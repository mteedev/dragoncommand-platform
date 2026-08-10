# DragonCommand — Roadmap

> This roadmap reflects the current development trajectory of DragonCommand.
> Items may shift as priorities evolve. Watch this repository for updates.

---

## Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Complete |
| 🔄 | In Progress |
| 📋 | Planned |
| 🗓️ | Future |
| 💰 | Paid Add-On Module |

---

## Phase 1 — The Egg ✅
*Foundation, infrastructure, authentication, public site shell*

### Infrastructure
- [x] Turborepo monorepo with pnpm workspaces
- [x] Package architecture (db, auth, opensim, validators, email, logger, ui)
- [x] PostgreSQL schema — 12 tables (DC core + better-auth)
- [x] Systemd services (auto-start, auto-restart on crash)
- [x] SSL on all domains (Let's Encrypt + certbot auto-renewal)
- [x] Nginx reverse proxy (panel + public site)
- [x] Self-hosted email (Postfix + OpenDKIM + DKIM/SPF/DMARC DNS)
- [x] Git + GitHub (private dev repo)

### Authentication
- [x] better-auth (email + password, session management)
- [x] Cross-subdomain session cookies (one login, all subdomains)
- [x] Rate limiting (5 attempts / 15 min lockout)
- [x] Auth middleware (panel locked — Drake+ rank required)
- [x] Dragon Rank system (Hatchling → DragonMaster)
- [x] Two-stage account architecture (web account → avatar creation)
- [x] DragonMaster account provisioning

### OpenSim Bridge
- [x] Robust schema version detector (NGC_0922 / TRANQUILITY_0933 / LEGACY)
- [x] MySQL connection pool manager (per grid_id)
- [x] User queries (getUserByName, getUserByUUID, checkNameAvailable)
- [x] Region queries (getAllRegions, getRegionsByOwner, getRegionCount)
- [x] Online presence query (getOnlineAvatarCount via Presence table)
- [x] Avatar writer (transactional: UserAccounts + auth + 15 inventory folders + avatarappearance)

### Public Grid Website
- [x] Hero landing page (grid branding, stats, CTAs)
- [x] Features section
- [x] CTA section
- [x] Footer with DragonCommand watermark
- [x] Navigation (desktop + mobile responsive)
- [x] Registration page (gated — REGISTRATION_OPEN flag)
- [x] Login page

### Resident Portal (Shell)
- [x] Portal layout (sidebar nav, top bar, sign out)
- [x] /me dashboard (avatar status, quick links, grid connection info)
- [x] /me/settings (password change, danger zone)
- [x] Stub pages: /me/profile, /me/friends, /me/inventory, /me/currency, /me/regions

### Admin Panel (Shell)
- [x] Dashboard shell (sidebar, header, dark/light toggle, dragon theme)
- [x] Login page (locked — auth required)
- [x] Command Center page (stat cards — stub)
- [x] DragonCommand watermark (persistent, non-removable)

---

## Phase 2 — The Hatchling 🔄
*Live grid data, avatar creation, email verification, Tailscale bridge*

### Infrastructure
- [ ] Tailscale mesh (VPS ↔ Proxmox home server)
- [ ] MS Axiom: Standalone Hypergrid → Grid Hypergrid conversion
- [ ] MariaDB network binding update (Tailscale interface)
- [ ] Robust DB live connection from VPS

### Authentication
- [ ] Email verification (Postfix port 25 — Interserver ticket JBX-817-46620)
- [ ] Email bounce webhook (instant ghost account purge)
- [ ] Password reset flow (email-based)
- [ ] Ghost purge cron (24hr unverified, 30-day no-avatar, 180-day dormant)

### Avatar Creation Flow
- [ ] /create-avatar — Step 2 UI (name picker + availability check)
- [ ] Avatar name validation (whitelist regex, reserved names, grid deny list)
- [ ] Appearance picker (system avatar selection)
- [ ] Stage 2 Robust DB write (UserAccounts + auth + inventory + avatarappearance)
- [ ] Welcome page + next steps (download Firestorm, connect URI)
- [ ] Rank upgrade: Hatchling → Fledgling on avatar creation

### Resident Portal — Live Data
- [ ] /me — Live avatar status (Egg vs Fledgling vs active)
- [ ] /me/profile — Tabbed: Info / Friends / Balance / Picks
- [ ] /me/friends — Friends list from Robust Friends table
- [ ] /me/currency — Balance + transaction history
- [ ] /me/inventory — Folder tree (like OpenSim "Wifi" panel)
- [ ] /me/inventory — IAR download (permissions-filtered)
- [ ] /me/regions — My regions list (Fledgling+ with land)
- [ ] /me/regions/[uuid] — Region management panel
  - [ ] Region online/offline status
  - [ ] Restart region (AIRWOLF sequence)
  - [ ] OAR download
  - [ ] OAR upload
  - [ ] Region config view

### Admin Panel — Live Data
- [ ] Command Center stat cards (Regions / Avatars Online / Registered Users — live)
- [ ] Grid status widget (real-time online indicator)

---

## Phase 3 — The Fledgling 📋
*Full admin panel, user management, grid configuration*

### Admin Panel — User Management
- [ ] User list (search, filter by rank, status, avatar stage)
- [ ] User detail view (DC account + Robust account linked)
- [ ] Dragon Rank assignment UI (with audit trail)
- [ ] Account status management (suspend, reinstate, schedule deletion)
- [ ] Ghost Hunter panel (pending purge queue, manual override)
- [ ] Email bounce management

### Admin Panel — Region Management
- [ ] Region list (all regions, online status, owner, size)
- [ ] Region detail view
- [ ] Region restart (AIRWOLF)
- [ ] OAR backup / restore
- [ ] Region config editor

### Admin Panel — Grid Configuration
- [ ] Setup wizard (first-boot grid config)
- [ ] Grid identity (name, logo, branding colors, login URI)
- [ ] Registration mode (closed / invite_only / moderated / open)
- [ ] Ghost purge timeline configuration
- [ ] Email from-name / from-address
- [ ] Grid name deny list management
- [ ] System avatar management (Picker, Banker, NPC roles)

### Admin Panel — Audit & Compliance
- [ ] Audit log viewer (filterable by event type, user, date range)
- [ ] Audit log export (CSV)

### System Avatars
- [ ] Picker avatar creation (for appearance selection during registration)
- [ ] Auto-add Picker names to deny list
- [ ] Banker avatar (for economy operations)

---

## Phase 4 — The Drake 🗓️
*Add-on modules, multi-tenancy, SaaS tier*

### Marketplace Module 💰
- [ ] Vendor application + terms agreement flow
- [ ] Vendor dashboard (product management, sales history, payouts)
- [ ] Vendor storefront (public-facing product listings)
- [ ] In-world delivery system (LSL vendor → API → inventory delivery)
- [ ] Product categories + search
- [ ] Resident purchase flow
- [ ] Grid operator marketplace settings

### Events Module 💰
- [ ] Public events calendar
- [ ] Event creation (staff+)
- [ ] GateCrashers.Events integration
- [ ] Event RSVP / attendance tracking
- [ ] In-world event announcements (LSL bridge)

### Land Sales Module 💰
- [ ] Parcel listing (owner self-service)
- [ ] Parcel purchase flow
- [ ] Rental management (recurring billing)
- [ ] Land office dashboard (grid admin)

### Partner System Module 💰
- [ ] Affiliate/referral link generation
- [ ] Referral tracking + attribution
- [ ] Partner dashboard (clicks, conversions, commissions)
- [ ] Grid operator partner settings

### Economy Dashboard Module 💰
- [ ] Grid-wide transaction history
- [ ] Balance management (admin adjustments)
- [ ] Economy reports + exports
- [ ] Gloebit / OMC / custom economy bridge

### Multi-Tenant & SaaS
- [ ] Grid onboarding wizard (new grid self-service)
- [ ] Per-grid branding (logo, colors, domain)
- [ ] Per-grid Add-On module toggle
- [ ] Billing / subscription management
- [ ] "Powered by DragonCommand" watermark (persistent — cannot be removed)
- [ ] DragonCommand.io hosted tier

### Advanced Bridge
- [ ] WebSocket real-time event streaming (LSL → API → WebSocket → UI)
- [ ] Grid event system (region crossing, login, logout, transactions)
- [ ] LibreMetaverse .NET sidecar (gRPC internal bridge)
- [ ] In-world HUD integration

---

## Phase 5 — The Ancient 🗓️
*Enterprise features, white-label, ecosystem*

- [ ] White-label installer (grid operators deploy under own brand)
- [ ] Multi-grid management (one DragonCommand, many grids)
- [ ] API documentation + developer portal
- [ ] Plugin/extension SDK
- [ ] Mobile app (iOS + Android — resident portal)
- [ ] Claude Tag / Discord bot integration
- [ ] NeverWorld Grid — Founder Edition deployment

---

## Not Planned

The following are explicitly out of scope for DragonCommand core:

- **Docker** — No Docker for V1. The OpenSimulator community runs bare-metal and VPS. DragonCommand deploys as systemd services.
- **Replacing OpenSimulator** — DragonCommand manages grids, it doesn't run them.
- **Single-grid lock-in** — Multi-tenant from day one.
- **Bulk/marketing email** — DragonCommand sends transactional email only (verification, password reset, lifecycle warnings). Never newsletters or marketing blasts.

---

<div align="center">

**༺🐲༻**

*One Platform. Total Control.*

</div>
