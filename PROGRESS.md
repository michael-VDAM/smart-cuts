# PROGRESS.md — Smart Cuts Current State

Last updated: 2026-05-28 (Session 5 — Waves 6→9 + debug pass)

## Live state
- **URL**: https://michael-vdam.github.io/smart-cuts/
- **Repo**: https://github.com/michael-VDAM/smart-cuts (public)
- **File**: ~5800 lines, single `index.html` + static assets (icons, manifest, sparky/)
- **Theme**: dark mode default on desktop, light mode default on phone (manual toggle persists). Both modes now **wood-forward** (warm walnut/espresso dark, parchment/oak light) — no more cold charcoal + cyber-yellow.
- **App icon**: square Sparky General (the bare character, no name/text). Used as the favicon, PWA icon, and home-page hero avatar.
- **Sparky icons**: 19 character icons in `sparky/` (256px each) — placed on every home tile, plus inline next to Wood Library / Projects / My Shop / Academy / Plans headers.
- **Installable**: PWA via `manifest.webmanifest` + apple-touch-icon → Add to Home Screen opens full-screen with the Sparky app icon.

## Session 5 wrap (2026-05-28) — 5 waves shipped, queue 9 → 5

| Wave | Commit | Ships |
|------|--------|-------|
| 6 | [d2256c7](https://github.com/michael-VDAM/smart-cuts/commit/d2256c7) | Parametric stripe formulas + strip-count input fix + drop haptic |
| 7 | [430d2d1](https://github.com/michael-VDAM/smart-cuts/commit/430d2d1) | Chevron / Basketweave / Diagonal end-grain patterns |
| 8 | [cf5fec1](https://github.com/michael-VDAM/smart-cuts/commit/cf5fec1) | Photo annotation on Projects |
| 8.1 | [7a1fafd](https://github.com/michael-VDAM/smart-cuts/commit/7a1fafd) | Debug-pass fixes (mobile picker scroll, print CSS hardening) |
| 9 | [fd6c8aa](https://github.com/michael-VDAM/smart-cuts/commit/fd6c8aa) | Wood Movement Calculator |

**Now 11 tabs** (added Movement). **Pattern picker has 10 patterns** (added Chevron / Basketweave / Diagonal). **Projects can hold annotations** (arrows, circles, text labels — non-destructive SVG overlay). **Parametric stripes** with formula textboxes + drum-pickable variables + 5 parametric presets that seed `x` and rewire on the fly.

## Features shipped (11 tabs)

### 1. Home
- App logo (lightbulb PNG) + title
- Tile navigation to other tabs
- Stat summary

### 2. Cutting Board
- **Standard mode**: 9 presets (mini → XL Butcher), shows only Thickness + Qty
- **Custom mode**: full L/W/T inputs + Settings (kerf, surface loss, buffer %)
- **End grain**: 10 patterns (checker, brick, stripe, plaid, 3D cube, herringbone, chevron, basketweave, diagonal, random)
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

## Session 4 — Bright Cuts rename + huge feature wave (2026-05-28)

Twenty-six commits in one session. Major themes:

### Brand + identity
- **Renamed Smart Cuts → Bright Cuts** (display name only — repo + Pages URL kept as `smart-cuts/` so existing PWA installs survive). All copy updated: header, manifest, README, copy-plan exports.

### New tabs
- **Calculator tab + always-on 🧮 header shortcut.** Wood-fraction math (add / subtract / multiply / divide). Tap "Enter value" → drum picker. Big copper result + expression line + history. Internal math in inches; output snaps to lowest-denominator power-of-2 fraction up to 64ths (so 2 1/16" − 3/32" = 1 31/32" exact). Honors Imperial/Metric. Header shortcut accessible from any page.
- **Lumber Prices tab.** Per-species $/bf editor with All/Common/Domestic/Figured/Exotic filter + search + "modified" highlight. New `priceFor()` helper overrides the SPECIES_PALETTE defaults everywhere. Cloud-synced.

### Measurement system
- **Imperial / Metric toggle** in the ⋯ menu. Internal storage stays inches; display unit drives every input + dim() output. Step changes (1/8" ↔ 1mm). Save/load preserves inches in localStorage so toggling never corrupts data. Toggling re-converts every measurement input live. 25 static + dynamic inputs covered.
- **Drum picker for all measurements.** iOS-style bottom-sheet with two scroll-snap columns (whole + fraction in imperial, cm + mm in metric). 1/16" snap (was 1/8"). Mask fade + center-line markers. Drum-pickable everywhere: Cutting Board, Furniture, Optimizer (static + dynamic rows), Strip widths, Project form, Calculator.
- **Unit pills** (IN / MM) on every measurement label so you always know what unit you're in.

### Cutting Board upgrades
- **Linked stripe widths** — strips at the same width are implicitly linked; editing one ripples to matched siblings (hold Alt to bypass). Linked rows highlight with accent border + "⛓ ×N" pill.
- **Ratio template chips** above the strip list: Halves, Sym 5, Sym 7, Golden, Golden 5. Formula-driven layouts that fill the panel width with 1/16" snap.
- **Pattern picker overhaul** — replaced the 7-button grid with a tappable preview card → bottom-sheet picker showing each pattern as a labeled mini SVG thumbnail. New `PATTERN_CATALOG` makes adding patterns trivial.
- **Standard sizes grid fix** — was wrapping 2/1/2/1 on phone; now stays 3-col on phone for clean 3 rows of 3.

### Wood Library
- **Tree identification per species** — new "The Tree" section in each card with stylized SVG silhouette + arborist description (height, leaves, bark, distinguishing features). 7 silhouette shapes: broad / oval / narrow / conifer / cypress / spreading / birch.
- **Regional detail per species** — new "Where It Grows" section with specific states/countries, climate, conservation notes. 18 species filled in (Walnut, Maple, Cherry, oaks, Ash, Hickory, Alder, Birch, Cedar, Cypress, Pine, Poplar, Soft Maple + 4 exotics). Remaining ~40 species progressively.
- "Edit prices" link now points to the Lumber Prices tab.

### Home page
- **Sectioned home tiles** — Design / Catalog / Learn / Shop. Design now 3-col (Cutting Board / Furniture / Optimizer); Catalog 2-col (Plans / Projects); Learn (Wood Library / Academy); Shop (My Shop / Lumber Prices). Calculator joined as a 4th Design tile (2×2 layout).

### Visual + UX polish
- **Light-mode input contrast** — text inputs now sit a notch darker than the page background with a stronger border so the box outline is visible.
- **Standard tab page headers** — Cutting Board / Furniture / Optimizer get a compact Sparky+title+description block at top of the input column.
- **iOS status bar fix** — switched apple-mobile-web-app-status-bar-style from black-translucent to default so iOS reserves a separate strip instead of overlaying.
- **Manifest theme_color updated** to new walnut + meta theme-color with light/dark media queries.
- **Tab strip auto-scrolls** the active tab into view (no more invisible-active when off-screen).
- **Title-with-quote bug fix** — plan titles like `Cabinet 30"×24"d` no longer truncate at the first `"` in HTML attributes (added `escapeHtml()` wrapping everywhere).
- **Desktop polish** — tabs + action buttons + brand subtitle nowrap on desktop, no more 2-line wraps.

### Commits (in order)
1. Bright Cuts rename + Standard headers + Standard sizes grid + light-mode contrast + Home sections + Lumber Prices
2. Wave 2: Linked stripe widths + Ratio templates
3. Wave 3 part 1: Imperial / Metric unit toggle
4. Wave 3 part 2: Scroll-wheel (drum) measurement picker
5. Polish pass: status bar + mobile/desktop refinements
6. 1/16" drum step + new Calculator tab
7. Always-available 🧮 calculator shortcut in the header
8. Drum picker on every length/width/thickness field
9. Pattern picker overhaul — bottom-sheet with thumbnails
10. Wood Library: regional detail + tree-identification per species
11. Wave 5: Custom species + Build timer + Shop-ready print + Haptic feedback

### Wave 5 (the last thing shipped in this session)
- **Custom species** — "+ Add custom species" on Lumber Prices opens a modal with name + color picker + Janka + $/bf. Custom entries get `cat:'custom'`, "★ CUSTOM" badge, and blend into the cutting-board species picker alongside the 56 Mimms species via a new `allSpecies()` helper. Edit/delete inline. New cloud collection `customSpecies`.
- **Build timer per Plan** — `{ accumulated: ms, startedAt: ts|null }` per plan. Start / Pause / Reset on every Plan card with live ticking display. Only ONE plan times at once. Header pill shows "● 12m 34s" when any timer is running. Assigning a plan to a Project auto-fills the project's hours field from the timer.
- **Shop-ready print** — `🖨 Print cut sheet` button next to Save Plan. @page letter, 0.5in margin. Hides every interactive control. Branded print-header injected via `beforeprint` hook with weekday-formatted date.
- **Haptic feedback** — `navigator.vibrate()` at low ms on tab switches, pattern picks, drum snaps, calculator operators, save plan. Toggle in ⋯ menu. Android honors it; iOS Safari silently ignores.

## Session 5 (2026-05-28) — shipped

- **Parametric stripe pattern** (queue item #1 done). Variable panel above # of Strips with drum-pickable values + add/remove buttons. Every strip row now has a **formula textbox** (e.g. `x`, `x/2`, `2x+y`, `x*phi`) + a **computed-width display**. Built-in constant `phi = 1.618033988749`. Same formula = implicit link (replaces same-width linking) with the `⛓ ×N` pill. Five parametric presets seed variables + formulas: Halves (`x · x/2 · x`), Sym 5 (`x · x/4 · x/2 · x/4 · x`), Sym 7 (extends Sym 5), Golden (`x · x*phi · x`), Golden Accent (`x*phi · x · x · x · x*phi`). Non-parametric presets (Solid/Single/Paired/Triple/Etsy/Uniform) use literal-number formulas. Old saves migrate cleanly via `ensureStripFormulas()`. Auto-fit converts formulas back to literal numbers (locks the layout). Tradeoff: parametric presets can drift up to 1/16" off finalW — the total bar shows it honestly + offers Auto-fit.
- **Strip count input bug fixed** — deleting the "4" in "# of Strips" used to instantly reset to "1" because oninput committed on every keystroke and refreshStripList re-wrote the input value mid-edit. Now uses `onchange` (commits on blur/Enter only), with a focus-aware writeback + onblur fallback. Can now clear and retype any number without the field fighting you.
- **Haptic removed entirely** — iOS Safari permanently blocks `navigator.vibrate()`, so the toggle + 7 vibration sites were dead weight on Michael's PWA. Cleaner without it. Restorable from git if Android users ever matter.
- **Three new end-grain patterns** (queue item #2 done): **Chevron** (mirrored V-point stripes — like herringbone but V tips align cleanly), **Basketweave** (2×2 mega-blocks with alternating grain orientation — horizontal-line cells vs end-grain-dot cells), **Diagonal** (45° bands of alternating species). Each has its own thumbnail in the picker, color logic in `tileColorFor`, build-step description in Phase 2 glue-up, and (for chevron + basket) special grain-line rendering in `svgFinishedBoard`. Picker now shows 10 patterns total.
- **Photo annotation on Projects** (queue item #3 done). Non-destructive — annotations are stored as normalized 0–1 coords on the project record, rendered as a SVG overlay on top of the photo. Four tools: **↗ Arrow** (tap start, tap end), **○ Circle** (tap center, tap edge), **T Text** (tap → prompt), **✕ Delete** (tap any annotation to remove). Four colors: red / yellow / blue / white. Editor is a full-screen modal (95vw × 95vh) reachable via an **✏ Annotate** button on the project detail page (only shown when the project has a photo). Cancel discards edits; Done commits. The detail view shows the saved annotations as an inline SVG overlay over the photo. Storage cost is tiny — a few floats per annotation, no canvas re-rasterizing.
- **Debug pass** (between waves): mobile pattern-picker bottom-sheet was overflowing viewport on mobile (10 cards too tall), pushing Cancel/Done off-screen. Now flex-column with max-height 88vh + internal scroll; header stays sticky. Print CSS hardened to explicitly hide `.drum-overlay`, `.modal-backdrop`, and `#annot-modal` so any accidentally-open modal never leaks into prints. Verified migration from pre-formula saves, projects-without-annotations rendering, and regression-clean standard cutting board / custom species / build timer.
- **Wood Movement Calculator** (queue item #4 done). New `Movement` tab + home tile. Inputs: species (dropdown of 32 species with published USDA Wood Handbook coefficients, plus everything else under an "Other (using hardwood average)" optgroup), panel width (drum-pickable), grain orientation (Flat / Rift / Quarter), and winter + summer MC%. Output: predicted dimensional change formatted as a fraction (e.g. `3/16"`), tangential or radial coefficient used, ΔMC%, the literal calc string, plus a contextual interpretation that scales with severity ("Negligible" → "Plan for X expansion gap" → "Significant movement — this panel **must** float in its frame"). Each species shows a colored stability badge (very-stable through very-high) that matches its movement class. State persists across sessions in `woodshop-movement-v1`.

## Queue for next session (in priority order)

1. **Academy lessons → quizzes curriculum** — Michael will write content, I scaffold. Beginner → Apprentice → Journeyman → Master tracks. Each lesson = text + diagrams → quiz at the end. Progressive unlock.
2. **Plan share link** — generate short URL → opens a read-only plan on someone else's phone with "Import to my Bright Cuts" button. Small Supabase table keyed by short id.
3. **Global search (⌘K)** — one bar searches plans, projects, species, supplies.
4. **Hardware database** — fasteners, glues, finishes with prices. Pairs with Lumber Prices for true total cost.
5. **Fill out remaining ~40 species** with tree+region data (currently 18/58 covered).

## Voice + haptic features explicitly OFF the table (per Michael)
- No "Hey Sparky" voice commands. No Web Speech API. He didn't want them.
- Haptic feedback removed 2026-05-28 — iOS Safari permanently blocks `navigator.vibrate()` (Apple has refused to ship the Web Vibration API for ~10 years), so the feature was dead on Michael's iPhone PWA. Restorable from git if Android support ever becomes a priority.

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
