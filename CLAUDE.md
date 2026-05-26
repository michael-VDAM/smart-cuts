# CLAUDE.md — Bright Cuts Project Briefing

**Read this first** at the start of every session. Then read PROGRESS.md (what's done) and DECISIONS.md (why we built it this way).

## What this is
**Bright Cuts** — a single-file HTML app for woodworking. By **Michael Makes It Work** (Michael Ross's personal woodworking brand). Lives in `~/code/woodshop/` locally, pushed to https://github.com/michael-VDAM/bright-cuts, deployed to https://michael-vdam.github.io/bright-cuts/.

## Tech stack
- **One file**: `index.html` (~4700 lines including inline CSS + JS)
- **Vanilla JS** — no framework, no build step
- **localStorage** for persistence (per-device, no backend)
- **Canvas API** for photo auto-resize (1200px max, JPEG 0.82)
- **Inline SVG** for logos + cutting-board previews + diagrams

## File layout
```
~/code/woodshop/
├── index.html       ← the entire app
├── README.md        ← public-facing project overview
├── CLAUDE.md        ← THIS FILE (session briefing)
├── PROGRESS.md      ← what's done + what's queued
├── DECISIONS.md     ← key architectural choices
└── .gitignore
```

## index.html section navigation
Big sections are marked with banner comments. Use grep to find them:
```bash
grep -n "═══.*═══" index.html          # all banner section headers
grep -n "^// ─── " index.html          # subsections
```
Major sections in order:
- CSS: BASE → HEADER → LAYOUT → COMPONENTS (TOGGLES, FIELDS, SPECIES, etc.) → tab-specific (PROJECTS, MY SHOP, ACADEMY, WOOD LIBRARY, HOME) → MOBILE RESPONSIVE → PRINT
- HTML: header → 8 tab divs (home, board, furniture, optimizer, library, academy, shop, projects)
- JS: STATE → HELPERS → STORAGE → MODE & PATTERN → SPECIES UI → cutting board math/render → furniture → optimizer → academy → wood library → projects → supplies → init

## Conventions (don't break these)
1. **Live preview** — all input changes debounced 180ms then trigger re-render. No "Plan Build" or "Generate" buttons. Simplicity.
2. **localStorage keys are versioned** (`woodshop-planner-v4`, `woodshop-projects-v1`, etc.). DO NOT change key names without a migration — wipes user data.
3. **Yellow accent `#e8a838`** is the brand color. Dark mode default. Light mode has its own variable overrides (search `[data-theme="light"]`).
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
- Laptop: open https://michael-vdam.github.io/bright-cuts/ in browser
- Phone: Safari → above URL → Share → "Add to Home Screen" → app icon

## Where Michael's other Claude docs live
- **Global memory**: `~/.claude/projects/-Users-michaelross-code-core/memory/MEMORY.md`
- **Global skills**: `~/.claude/skills/` (per-user) + `~/.claude/plugins/anthropic-skills/skills/`
- **Core platform**: `~/code/core/` (Validator Digital infrastructure)
- **VD projects**: `~/Documents/Claude/Projects/` (Validator Digital work projects + Woodworking reference docs)
- **Woodworking reference**: `~/Documents/Claude/Projects/Woodworking/.claude/skills/{wood-expert,tool-expert,finishing-specialist,maintenance}/references/` — these informed the Wood Library + My Shop content

## Quick orientation prompts for future sessions
- "Let's work on Bright Cuts" or "Let's improve the woodshop app" — triggers reading these 3 files
- Always cd to `~/code/woodshop/` before edits
- This is NOT a VD project, so vd-session-lifecycle skill should NOT fire

## Tone preferences (from user feedback)
- **Plain English** at decision time (Michael's emphasis)
- **Simplicity wins** — resist feature bloat; prefer hiding to adding
- **Commit one recommendation**, don't stack 3 options unless asked
- **Verify before asserting** — 30s of research saves debugging
- **Trim before adding** — beware doc bloat
