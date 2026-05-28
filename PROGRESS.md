# PROGRESS.md — Smart Cuts Current State

Last updated: 2026-05-27 (Session 3 — Sparky visual overhaul + Plans feature)

## Live state
- **URL**: https://michael-vdam.github.io/smart-cuts/
- **Repo**: https://github.com/michael-VDAM/smart-cuts (public)
- **File**: ~5100 lines, single `index.html` + static assets (icons, manifest, sparky/)
- **Theme**: dark mode default on desktop, light mode default on phone (manual toggle persists). Both modes now **wood-forward** (warm walnut/espresso dark, parchment/oak light) — no more cold charcoal + cyber-yellow.
- **App icon**: square Sparky General (the bare character, no name/text). Used as the favicon, PWA icon, and home-page hero avatar.
- **Sparky icons**: 19 character icons in `sparky/` (256px each) — placed on every home tile, plus inline next to Wood Library / Projects / My Shop / Academy / Plans headers.
- **Installable**: PWA via `manifest.webmanifest` + apple-touch-icon → Add to Home Screen opens full-screen with the Sparky app icon.

## Features shipped (9 tabs)

### 1. Home
- App logo (lightbulb PNG) + title
- Tile navigation to other tabs
- Stat summary

### 2. Cutting Board
- **Standard mode**: 9 presets (mini → XL Butcher), shows only Thickness + Qty
- **Custom mode**: full L/W/T inputs + Settings (kerf, surface loss, buffer %)
- **End grain**: 7 patterns (checker, brick, stripe, plaid, 3D cube, herringbone, random)
- **Face grain**: strip pattern with # of strips + per-strip species + width editor
- **56 species** with prices, dynamic species picker (click ≡ for catalog)
- Edge profiles (chamfer, 1/8" / 1/4" / 1/2" roundover) + juice groove options
- Buffer % allowance (10/20% defaults by mode)
- 7-step build plan with measurements + SVG diagrams per step
- Stock Lumber hidden in UI (defaults 4/4 × 6" × 36") — math still uses it
- Copy plan to clipboard

### 3. Furniture
- 3 types: Cabinet (base/wall/tall), Bookshelf, Drawer Box
- 9 drawer joinery options (butt, pocket, dowel, rabbet, lock, box, through dovetail, half-blind dovetail, sliding dovetail)
- Door styles (none, slab, shaker) with proper part calculation
- Live front-view + isometric previews
- Parts list with material tags
- "Send to Stock Optimizer" button

### 4. Stock Optimizer
- Bin-packing algorithm with kerf
- Material-aware (matches piece mat to stock mat, "any" = wildcard)
- SVG cut diagrams per board
- Efficiency stats + unplaced warning

### 5. Wood Library
- 56 species (Mimms Lumber inventory: domestic, figured, exotic)
- Full encyclopedia per species (Latin, origin, Janka with visual bar, grain, color, workability, uses, finishing gotchas)
- Filter: All / Domestic / Figured / Exotic with counts
- Search box (name + Latin)

### 6. Academy (Quiz)
- **8 categories**: Wood ID, Trivia, Joinery, Tools, Process, Safety, Finishing, Sharpening
- **~100 questions** total
- Welcome → quiz → results flow with per-category breakdown
- **Best-score persistence per category** (★ Best 80%)
- Rank levels: Beginner → Hobbyist → Apprentice → Journeyman → Master Woodworker
- Review-missed-questions section

### 7. My Shop
- 7 categories: Power Tools, Blades & Bits, Jigs, Hand Tools, Clamps, Finishing, Safety
- Tool-for-the-Job matrix (21 operations → best tool)
- Per-item photo upload (click camera icon)
- **My Supplies** filter: user-editable inventory with CRUD form (Walrus Oil, Titebond, etc.)

### 8. Plans (design catalog) — NEW
- "+ Save Plan" button on the Cutting Board and Furniture preview cards captures the current spec (species, dims, pattern, parts list) as a snapshot
- Plans land in **Unassigned** by default; when you finish building, **Assign to project →** moves the plan into "Built ✓" and links it to a Project
- Plan card shows: Sparky icon (matching the design type), generated title (e.g. "Walnut + Maple checkerboard 12"×8""), type/species sub, save date, action buttons
- Assign-to-project modal lists existing projects or "+ New project" (pre-fills the project form from the plan's species/dims and auto-links after save)
- Project detail page shows a "Linked plans" section with Unlink action
- Storage: `woodshop-plans-v1` localStorage; synced via existing cloud sync (added `plans` collection to CLOUD_COLLECTIONS)

### 9. Projects (catalog)
- Photo upload (auto canvas-resize)
- Title, date, project type (11 types with emoji)
- Multi-select species from palette with color chips
- Stain dropdown (10 Minwax options + supplies)
- Finish dropdown (Walrus Oil, mineral oil+beeswax, common finishes + user supplies)
- Coats, dimensions, hours, sale price, sold date, description
- List/detail views with edit/delete

## Session 3 visual + feature overhaul (2026-05-27)

- **Square Sparky General app icon** — center-padded the wide source to square (cream bg, no text), regenerated apple-touch-icon / icon-192 / icon-512 / favicon. The app now installs with the bare-character Sparky on the home screen.
- **Wood-forward color palette** — dark mode is now warm walnut/espresso (bg `#18120c`, panel `#1f1812`, accent honey-amber `#d4a056`). Light mode is richer parchment with deeper copper-amber accent (`#b56a1f`). Replaced all hardcoded `rgba(232,168,56,...)` and the cold-blue `rgba(74,158,255,...)` with the new amber + muted slate. The dark `.finished-preview` gradient is now walnut, not charcoal.
- **Mobile-first home page** as app-style launcher — 2-col tile grid on phone, 3 on tablet, 4 with descriptions on desktop. Each tile is a square Sparky-iconed card. The hero is a compact circular Sparky avatar + title + tagline.
- **Header collapse on phone** — Sign in / Theme / Print / Reset all fold into a single ⋯ menu button. Brand subtitle hidden on phone (redundant with home hero). Tab strip gets scroll-snap and hidden scrollbar on phone.
- **Sparky icons throughout** — 19 256px icons in `sparky/` (general, cutting-board, furniture, calculator, wood-selection, academy, tools, camera, plans, pencil, shelves, table-design, finishes, measuring-tools, moisture-reader, safety, screws, thickness, cnc). Currently used: 1 per home tile, 1 per tab hero (Wood Library, Projects, My Shop, Academy, Plans).

## Other shipped
- **Light/dark mode** with persistence — **defaults to light on mobile (≤820px), dark on desktop**; manual toggle overrides
- **Mobile app polish** — sticky header, iOS safe-area insets (notch/home-indicator), bigger tap targets, hid "Live preview" label on phones
- **Cloud sync (DEPLOYED, login test pending)** — Supabase-backed cross-device sync for projects/supplies/shop photos is live in the deployed app. Project: `brrtfvfilcaoktykrijt` in Michael's **separate private Supabase org** (NOT the Validator Digital org — the MCP connection cannot reach it; Michael runs any SQL/auth changes himself via the dashboard). Table `smartcuts_state` created + RLS verified (anon REST returns `[]`, HTTP 200). Auth = email magic-link; redirect URL set to the Pages URL. **Still unverified:** the actual end-to-end magic-link login + two-device sync test (needs Michael's email). Pick up here next session. See DECISIONS 2026-05-27.
- **Mobile responsive** (@media 820px + 480px breakpoints)
- **Print stylesheet** with `print-color-adjust: exact` for swatches
- **localStorage** persistence for all user state
- **PWA install** — manifest + apple-touch-icon + apple-mobile-web-app meta; standalone full-screen on phone with custom lightbulb icon

## Known issues / fixes deferred
- (none currently — broke navigation once with missing `};`, fixed)

## Deferred features (not yet built)
1. **Export / Import backup** — JSON download/upload for cross-device sync (offered to user, awaiting "yes")
2. ~~**App rename**~~ — DONE 2026-05-27: renamed "Bright Cuts" → "Smart Cuts" (display name, repo slug, and Pages URL all updated)
3. ~~**Real cloud sync**~~ — DONE 2026-05-27: Supabase magic-link sync for projects/supplies/shop photos, deployed (login test pending). See "Other shipped".
4. **Photo-to-pattern** — upload board design photo, detect grid, auto-set pattern. Originally requested early on.
5. **Cabinet drawer faces** — currently no separate drawer face panels in cabinet builder. Real kitchen drawers need them.
6. **Multi-cabinet layouts** — "3 wall cabinets across 90 inches" — not yet supported.
7. **3D Cube SVG rendering** — algorithm is right but visual uses square tiles, not hexagonal cube projections. Build notes are accurate (60° miter cuts).
8. **More quiz categories** — Sourcing, Wood Science deep dive, Project Estimation, Workshop Setup
9. **Lumber cost calculator** — total board-feet → cost breakdown by species (math exists, no dedicated UI)
10. **Stock photos for shop items** — can't auto-fetch from Amazon/HD due to copyright/CORS. Workaround: user uploads screenshots manually.

## Last few user feedback notes
- Removed: Plan Build button, Generate Parts List button (live preview redundant)
- Removed: Stock Lumber section visibility (uses defaults)
- Removed: Quick Layouts dropdown from strip pattern
- Fixed: Grain lines were vertical, now horizontal (along strip length)
- Fixed: Project form photo upload was wonky (label needed display:block)
- Renamed: Bright Cuts → Smart Cuts (2026-05-27)
- Replaced: 4 SVG logo variants retired → single PNG lightbulb logo (header + home + app icon)
- Added: PWA / Add to Home Screen install
- Added: Mobile responsive
- Added: GitHub Pages hosting
