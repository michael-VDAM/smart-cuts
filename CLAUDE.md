# CLAUDE.md — Bright Cuts Project Briefing

**Read this first** at the start of every session. Then read PROGRESS.md (what's done) and DECISIONS.md (why we built it this way).

## What this is
**Bright Cuts** — a single-file HTML app for woodworking, installable on phone via Add to Home Screen (PWA). By **Michael Makes It Work** (Michael Ross's personal woodworking brand). Lives in `~/code/woodshop/` locally (folder name unchanged), pushed to https://github.com/michael-VDAM/smart-cuts (legacy slug from a brief 2026-05-27 rename that's since been undone), deployed to https://michael-vdam.github.io/smart-cuts/. The app's display name is **Bright Cuts**; the `smart-cuts/` URL is kept only to avoid breaking the existing PWA install on Michael's phone.

## Tech stack
- **One file**: `index.html` (~8550 lines including inline CSS + JS) + static assets (icons, manifest, `sparky/` art, `species/` reference photos)
- **Vanilla JS** — no framework, no build step
- **localStorage** for persistence (per-device, no backend)
- **Canvas API** for photo auto-resize (1200px max, JPEG 0.82)
- **Inline SVG** for cutting-board previews + diagrams; **PNG app icon** for the logo (header, home hero, and home-screen install)
- **PWA**: `manifest.webmanifest` + apple-touch-icon + apple-mobile-web-app meta tags → standalone full-screen install on phone

## File layout
```
~/code/woodshop/
├── index.html             ← the entire app
├── manifest.webmanifest   ← PWA manifest (name, icons, standalone display)
├── apple-touch-icon.png   ← 180×180 iOS home-screen icon
├── icon-192.png           ← header logo + PWA icon
├── icon-512.png           ← home hero logo + PWA icon
├── favicon-32.png         ← browser tab favicon
├── sparky/                ← Sparky character art (256px PNGs), one per tab/tile
├── species/               ← Wood Library tree·leaf·bark photos (Wikimedia, PD/CC)
├── README.md              ← public-facing project overview
├── CLAUDE.md              ← THIS FILE (session briefing)
├── PROGRESS.md            ← what's done + what's queued
├── DECISIONS.md           ← key architectural choices
└── .gitignore
```
Icons are generated from the source logo via `sips` (center-crop to square → resize). Source: a Gemini-generated "Michael Makes It Work" lightbulb logo. `species/` photos are CC/PD images sourced from Wikimedia Commons — keep the author + license attribution that renders in each photo's lightbox caption.

## index.html section navigation
Big sections are marked with banner comments. Use grep to find them:
```bash
grep -n "═══.*═══" index.html          # all banner section headers
grep -n "^// ─── " index.html          # subsections
```
Major sections in order:
- CSS: BASE → HEADER → LAYOUT → COMPONENTS (TOGGLES, FIELDS, SPECIES, etc.) → tab-specific (PROJECTS, MY SHOP, ACADEMY, WOOD LIBRARY, WOOD ORIGINS, HOME) → MOBILE RESPONSIVE → PRINT
- HTML: header → 15 tab divs — home, board (Cutting Board), furniture, optimizer, calc (Calculator), frame (Picture Frame), todo (My To-Do), plans (My Plans), projects (My Projects), shop (My Shop), prices (Lumber Prices), hardware, library (Wood Library), origins (Wood Origins), academy. Grouped in nav + home as **Design / Workshop / Learn** via `NAV_GROUPS` (the single source of truth for grouping).
- JS: STATE → HELPERS → STORAGE → MODE & PATTERN → SPECIES UI → cutting board math/render → furniture → optimizer → calculator → picture frame → academy → wood library (+ `SPECIES_PHOTOS`) → wood origins (static HTML, no render) → projects → plans → supplies → hardware → to-do → init

## Conventions (don't break these)
1. **Live preview** — all input changes debounced 180ms then trigger re-render. No "Plan Build" or "Generate" buttons. Simplicity.
2. **localStorage keys are versioned** (`woodshop-planner-v4`, `woodshop-projects-v1`, etc.). DO NOT change key names without a migration — wipes user data.
3. **Yellow accent `#e8a838`** is the brand color = the **dark-theme** accent. The **light** theme uses `#a04f00` (burnt orange) — a deliberate split so the accent clears WCAG AA contrast on the parchment bg (the old `#b56a1f` failed at 3.36:1). Theme default is **dark on desktop, light on phone** (manual toggle persists). Light mode has its own variable overrides (search `[data-theme="light"]`); keep new accent-colored text legible in BOTH.
4. **Photos auto-resize** via `processPhotoFile()` — every photo upload route through this. Keeps localStorage sane.
5. **Standard vs Custom UI mode** on cutting board: `[data-ui-mode="standard"]` hides `.custom-only` + `.standard-hide`, `[data-ui-mode="custom"]` hides `.standard-only`. Stock Lumber is `display:none` always.
6. **`node --check` on the script** after large edits to QUIZ_QUESTIONS or any object literal — I broke navigation once by missing a `};`.

## Update workflow
```bash
cd ~/code/woodshop
# (Edit index.html)
git add index.html
git commit -m "describe change"
git push
```
GitHub Pages auto-deploys in ~30 seconds. Hard refresh on phone/laptop to see new version.

## How users access it
- Laptop: open https://michael-vdam.github.io/smart-cuts/ in browser
- Phone: Safari → above URL → Share → "Add to Home Screen" → installs full-screen with the lightbulb app icon

## Where Michael's other Claude docs live
- **Global memory**: `~/.claude/projects/-Users-michaelross-code-core/memory/MEMORY.md`
- **Global skills**: `~/.claude/skills/` (per-user) + `~/.claude/plugins/anthropic-skills/skills/`
- **Core platform**: `~/code/core/` (Validator Digital infrastructure)
- **VD projects**: `~/Documents/Claude/Projects/` (Validator Digital work projects + Woodworking reference docs)
- **Woodworking reference**: `~/Documents/Claude/Projects/Woodworking/.claude/skills/{wood-expert,tool-expert,finishing-specialist,maintenance}/references/` — these informed the Wood Library + My Shop content

## Quick orientation prompts for future sessions
- "Let's work on Smart Cuts" or "Let's improve the woodshop app" — triggers reading these 3 files
- Always cd to `~/code/woodshop/` before edits
- This is NOT a VD project, so vd-session-lifecycle skill should NOT fire

## Tone preferences (from user feedback)
- **Plain English** at decision time (Michael's emphasis)
- **Simplicity wins** — resist feature bloat; prefer hiding to adding
- **Commit one recommendation**, don't stack 3 options unless asked
- **Verify before asserting** — 30s of research saves debugging
- **Trim before adding** — beware doc bloat
