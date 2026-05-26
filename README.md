# Bright Cuts

A single-file woodworking companion app by **Michael Makes It Work**.

🪵 Plan cutting boards (end-grain + face-grain) • Furniture builder • Stock optimizer • Wood encyclopedia (56 species) • Workshop quiz academy • Tool inventory • Project catalog • Supplies tracking

## Live site
👉 https://USERNAME.github.io/bright-cuts/

*(URL will be set after Pages enable)*

## Run locally
```bash
open index.html
```

That's it — no build step, no dependencies. Just a single HTML file with inline CSS + JS.

## Data
Everything is stored in browser **localStorage** — per device. Projects, photos, supplies, quiz scores, theme preference, and logo choice all live in your browser. No backend, no tracking, no analytics.

## Update workflow
```bash
git add index.html
git commit -m "describe change"
git push
```
GitHub Pages auto-deploys within ~30 seconds. Hard refresh (`Cmd+Shift+R`) on your phone/laptop to see the new version.

## Stack
- Single HTML file (~4600 lines)
- Vanilla JS, no framework
- localStorage for persistence
- Canvas API for photo resizing (auto 1200px max, JPEG 0.82)
- SVG inline rendering for cutting board previews, logos, diagrams

## Features
- **Cutting Board planner** — end + face grain, 7 patterns (checker, brick, stripe, plaid, 3D cube, herringbone, random), 9 standard sizes, multi-species with prices, edge profiles, juice groove
- **Furniture builder** — base/wall/tall cabinets with door styles, bookshelves, drawer boxes with 9 joinery types
- **Stock Optimizer** — bin-packing for sheet goods + lumber with kerf + material matching
- **Wood Library** — 56 species (Mimms Lumber inventory) with full encyclopedia: Latin name, origin, Janka, grain, color, workability, uses, gotchas
- **Academy** — 100+ quiz questions across 8 categories with per-category best-score tracking
- **My Shop** — tool inventory + 10 custom jigs + tool-for-the-job matrix + editable supplies
- **Projects** — photo catalog with species, finish, coats, dimensions, hours, sale price tracking

## License
Personal project. Not licensed for commercial use without permission.

Built with [Claude Code](https://www.claude.com/product/claude-code).
