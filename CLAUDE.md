# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project purpose

`eddy-www` is the central landing page for the **eddy-apps** ecosystem at `eddy-apps.com`. It is a static HTML site whose job is to represent the brand and route visitors to the individual eddy-apps subdomains.

## Tech stack

**Plain HTML + CSS. No build step, no framework, no package manager.**

Decided 2026-05-21. The site is small enough that a Node toolchain would be more overhead than benefit. Pages are written directly as `.html` files and deployed by copying them onto a webspace.

Consequence to accept: shared markup (header, footer with the Impressum/Datenschutz/Nutzungsbedingungen links, app-grid) **is duplicated across every page**. When you change the footer, change it in each `.html` file. If this duplication ever becomes painful, the escape hatch is to migrate to a static-site generator (Astro or 11ty were the runners-up) — but do not introduce one without asking first.

Do **not** add: `package.json`, build scripts, CSS preprocessors, JS bundlers, or CI pipelines unless the user explicitly asks. CSS goes in plain `.css` files. If interactivity is ever needed, vanilla JS in `<script>` tags — no frameworks.

## Subdomain map

All eddy-apps live under `eddy-apps.com`. The landing page must link to each:

| App | Code | Subdomain |
|---|---|---|
| Landing Page | — | `www.eddy-apps.com` |
| KanuEventPlanner | `kep` | `kanueventplanner.eddy-apps.com` |
| Camping Self Registration | `csr` | `campingselfregistration.eddy-apps.com` |
| River-DB | `rdb` | `riverdatabase.eddy-apps.com` |
| RiversAndKajaks | `rak` | `riversandkajaks.eddy-apps.com` |
| Shop | `shp` | `shop.eddy-apps.com` |
| Wiki | `wik` | `wiki.eddy-apps.com` |
| Fahrtenbuch | `efb` | `efb.eddy-apps.com` |
| Chat | `cht` | `chat.eddy-apps.com` |

More subdomains will be added over time — keep the structure additive.

## Brand

**Leitmetapher: „Kehrwasser"** — der ruhige Ort am Fluss, an dem Paddler kurz innehalten, sich sammeln und die nächste Passage planen.

Eddy is a tool for paddlers — people who get up early, who are happy when the water is right, and who are pragmatic. Not startup-glanz, not tech aesthetics. More like: *eine schöne Outdoor-App, die einfach funktioniert.*

Voice keywords: **ruhig · klar · wasserfarben-leicht · handwerklich solide · nicht verspielt, aber auch nicht steril**

What Eddy is **not**:
- not "corporate SaaS"
- not "fitness app mit Energiebalken"
- not "premium luxury"

Apply this voice to copy, visual choices, and component design alike. When in doubt, err on the side of quiet and clear over expressive. The audience reads German — copy should be in German unless there is a reason otherwise.

## Design system

Tokens (colors, type, spacing, radii, shadows, motion) live in [`docs/design-system/colors_and_type.css`](docs/design-system/colors_and_type.css). Documentation and usage rules are in [`docs/design-system/README.md`](docs/design-system/README.md) — read it before writing CSS or markup, and prefer `var(--token-…)` over hard-coded values. New tokens are added there and documented in the same PR.

## Regulatory requirements (DE / DSGVO)

Every public page must include a footer linking to:
- Datenschutzerklärung
- Nutzungsbedingungen
- Impressum

These pages must exist and be reachable before the site goes live. Treat them as launch-blockers, not nice-to-haves.

**Current state of the Legal pages:** `impressum.html`, `datenschutz.html`, and `nutzungsbedingungen.html` contain **template content with `<mark class="todo">[bitte ergänzen: …]</mark>` placeholders**, plus a visible `.legal-note` warning banner at the top. They are **not** legally final. Before launch: replace all placeholders with real data and have the result reviewed by a competent person (lawyer or vetted DSGVO generator). Do not remove the warning banner until that review has happened.

### Cookie-banner discipline

The site currently ships **without a cookie banner**, which is only acceptable because:

- no analytics, no tracking pixels, no remarketing
- fonts (Nunito Sans) are served locally from `docs/design-system/fonts/`
- no embeds (YouTube, Maps, Twitter, etc.)
- no third-party cookies of any kind

If *any* of these changes — even adding Google Fonts CDN or a single YouTube iframe — the no-banner assumption breaks and consent must be re-evaluated. Don't introduce such dependencies without first updating `datenschutz.html` and deciding on a consent mechanism. The Datenschutz page calls this out explicitly in section 5.

## Build / run / test

There is no build step. To preview locally, open the `.html` files directly in a browser, or run any static file server from the repo root, e.g.:

```powershell
python -m http.server 8000
```

Then visit `http://localhost:8000/`.

Deployment is a plain file copy to the target webspace.
