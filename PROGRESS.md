# PROGRESS.md — Bright Cuts Current State

Last updated: 2026-05-26 (Session 1 close)

## Live state
- **URL**: https://michael-vdam.github.io/bright-cuts/
- **Repo**: https://github.com/michael-VDAM/bright-cuts (public)
- **File**: ~4700 lines, single `index.html`
- **Theme**: dark mode default; light mode toggle in header
- **Active logo**: cheerful (smiling lightbulb + hammer + sparkles)

## Features shipped (8 tabs)

### 1. Home
- 4 logo variant picker (cheerful / bold / spark / outline)
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

### 8. Projects (catalog)
- Photo upload (auto canvas-resize)
- Title, date, project type (11 types with emoji)
- Multi-select species from palette with color chips
- Stain dropdown (10 Minwax options + supplies)
- Finish dropdown (Walrus Oil, mineral oil+beeswax, common finishes + user supplies)
- Coats, dimensions, hours, sale price, sold date, description
- List/detail views with edit/delete

## Other shipped
- **Light/dark mode** with persistence
- **Mobile responsive** (@media 820px + 480px breakpoints)
- **Print stylesheet** with `print-color-adjust: exact` for swatches
- **localStorage** persistence for all user state

## Known issues / fixes deferred
- (none currently — broke navigation once with missing `};`, fixed)

## Deferred features (not yet built)
1. **Export / Import backup** — JSON download/upload for cross-device sync (offered to user, awaiting "yes")
2. **App rename** — suggested "Workbench", "The Bench", "Sawdust", "Shop Companion" — user not yet decided
3. **Real cloud sync** — Supabase/Cloudflare KV for cross-device data sync (only needed if Export/Import is too manual)
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
- Added: 4 logo variants on home page
- Added: Mobile responsive
- Added: GitHub Pages hosting
