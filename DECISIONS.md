# DECISIONS.md — Bright Cuts Architecture Choices

One-line entries. Add new entries at top, dated.

## 2026-05-26
- **Single HTML file, no build step** — easier hosting (works from `file://` or any static host), offline-capable, no dependencies to break. Tradeoff: 4700 lines is getting big, but search/navigation via grep is fine.
- **Vanilla JS, no framework** — same reason: no build, no node_modules, no version churn. Code is readable to anyone who knows JS.
- **localStorage for ALL user data** — no backend means no server costs, no auth complexity, no privacy concerns. Tradeoff: per-device data, no cross-device sync. Acceptable for personal app; Export/Import or cloud sync can layer on later.
- **Photos auto-resized to 1200px max JPEG 0.82** — keeps localStorage under quota (~5-10MB). User can fit 20-50 projects with photos before hitting cap. Quality is sufficient for portfolio reference.
- **Brand color `#e8a838` (warm gold-yellow)** — matches the lightbulb in the user's "Michael Makes It Work" logo. Light mode uses slightly darker `#c47a1a` for contrast on white.
- **Dark mode default** — most woodworkers/makers prefer dark UIs. Light mode optional, persists in localStorage.
- **App named "Bright Cuts"** — ties to lightbulb logo (bright/ideas) and woodworking (cuts). User considering rename (Workbench, The Bench, Sawdust, Shop Companion). Decision pending.
- **Removed Plan Build / Generate Parts buttons** — live preview made them redundant. "Simplicity wins" — user feedback.
- **Stock Lumber section hidden in cutting board UI** — defaults to 4/4 × 6" × 36" lumber. Hiding reduces cognitive load. Inputs still in DOM for math + save/load. Custom users who need different stock would have to know to override via JS (acceptable for power users).
- **Standard mode hides L/W inputs** — preset picks them. Only Thickness editable. Simplest possible flow for the 90% case.
- **Custom mode hides Standard Sizes** — clean separation of modes. Power user only sees what they need.
- **Strip Pattern: removed Quick Layouts dropdown, kept # of Strips** — user feedback "doesn't add value, only distracts." # of strips + per-strip editor is enough.
- **Grain lines run HORIZONTAL in face-grain preview** — matches real wood grain direction (along the strip's length). Originally drew vertical (bug, fixed).
- **Wood Library uses Mimms Lumber inventory (56 species)** — user's actual local source in Nashville. Categorized: domestic / figured / exotic.
- **Dynamic Project finish/stain dropdowns** — hardcoded common options + user's My Supplies in oil-wax/stain/finish categories. User can add Walrus Oil to supplies, it shows up everywhere relevant.
- **Quiz best-score persistence per category** — keyed by category, only updates when beating previous best. Shows "★ Best X%" on welcome.
- **Logo as inline SVG, not external image** — keeps single-file architecture intact. 4 variants user can switch between, persisted in localStorage.
- **Mobile breakpoints at 820px and 480px** — covers tablet + phone. Workspace stacks input → output vertically. Tabs scroll horizontally.
- **GitHub Pages hosting (not Netlify)** — user has GitHub account, prefers git push workflow over drag-and-drop. Version control for free. Auto-deploys ~30 sec.
- **Repo public** — no secrets in code. Easier for Pages, simpler permissions.
- **Author email = noreply GitHub email** — doesn't leak personal email in commit history of a public repo.
- **3-file Claude convention** (CLAUDE.md / PROGRESS.md / DECISIONS.md) — copied from Core's vd-session-lifecycle pattern. Future sessions read these at start to orient quickly.

## Reverted / things we tried that didn't work
- **3D Cube hexagonal SVG rendering** — attempted full hex projection. Math was right but visual was busy. Reverted to flat tiles + accurate build notes (60° miter cuts). Future work to render real hexagons.
- **Auto-fetching Amazon/HD product images** — researched, can't legally embed (copyright + CORS + URL rot). Switched to manual photo upload with category emoji fallback.
- **stockBoardsNeeded vs sum-of-per-species buffered** — initial math had rounding drift (ceil applied at both levels). Now total = sum of per-species buffered, consistent.
- **Wood library 'Oak' / 'Zebrawood' encyclopedia entries** — old keys preserved when palette renamed to 'White Oak' / 'Zebra Wood'. Dead data, not removed (no functional impact).
