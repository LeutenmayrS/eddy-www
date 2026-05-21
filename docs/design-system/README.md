# Eddy Design System

Single source of truth für Farben, Typografie, Spacing, Schatten und Motion der eddy-apps-Familie. Alle Tokens leben in [`colors_and_type.css`](./colors_and_type.css) als CSS Custom Properties (`--eddy-…`, `--space-…`, etc.).

Die Landing-Page `eddy-www` ist die Referenzimplementierung — andere eddy-apps (kep, csr, rdb, rak, …) sollen sich an denselben Tokens orientieren, damit das Ökosystem als eine Marke erlebbar bleibt.

## Leitidee

Die Tokens stützen die Marken-Leitmetapher **„Kehrwasser"** (siehe [`../../CLAUDE.md`](../../CLAUDE.md)): ruhige, klare, wasserfarben-leichte Oberflächen mit gelegentlichen warmen Akzenten. Die Wahl der Palette ist nicht beliebig:

- **River Blues** (`--eddy-50…900`) bilden das Rückgrat — Wasser, Ruhe, Tiefe.
- **Sand & Wood** (`--sand-50…400`, `--wood-700`) sind die warmen Gegenstücke — Ufer, Boot, Paddel. Sie kommen sparsam.
- **Sunset** (`--sunset-400…600`) ist der einzige laute Ton. *Maximal ein „Moment" pro Screen* — sonst verliert er seine Funktion.
- **Neutrals** sind absichtlich leicht warm, nicht reines Grau, damit Oberflächen nicht klinisch wirken.
- **Schatten** sind primary-dark-getönt (`rgba(20, 56, 72, …)`), **nie** reines Schwarz.

Was Eddy **nicht** ist: kein corporate SaaS, keine Fitness-App, kein premium luxury. Wenn ein Element diese Energie ausstrahlt, ist die Palette falsch eingesetzt — nicht die Palette das Problem.

## Verwendung

Das Stylesheet einbinden — alle Tokens stehen danach unter `var(--token-name)` zur Verfügung:

```html
<link rel="stylesheet" href="/docs/design-system/colors_and_type.css">
```

> Hinweis: Sobald der Produktiv-Pfad festgelegt ist (z.B. `/assets/design-system.css`), wird der Pfad oben angepasst. Bis dahin lebt die Datei unter `docs/`, weil sie der Dokumentation näher steht als dem Output.

In CSS:

```css
.card {
  background: var(--bg-surface);
  border: 1px solid var(--border-soft);
  border-radius: var(--radius-list-card);
  padding: var(--space-5);
  box-shadow: var(--shadow-sm);
}
```

In HTML — semantische Typo-Klassen direkt nutzen:

```html
<h1 class="eddy-h1">Kehrwasser</h1>
<p class="eddy-lead">Der ruhige Ort am Fluss.</p>
<span class="eddy-label">Kehrwasser</span>
```

## Farben

### River Blues — Primärpalette

| Token | Hex | Verwendung |
|---|---|---|
| `--eddy-50` | `#EEF5F9` | leichtester Tint, getönte Flächen (`--bg-tinted`) |
| `--eddy-100` – `--eddy-300` | | Hover-States, Backgrounds, dezente Akzente |
| `--eddy-400` | `#4E91B2` | sekundäre Buttons, Outlines |
| **`--eddy-500`** | `#2E7A9E` | **PRIMARY** — Aktionsfarbe, Links (`--fg-link`), Brand |
| `--eddy-600` | `#235F7D` | Hover / Pressed der Primary |
| **`--eddy-700`** | `#1B4B64` | **PRIMARY DARK** — Header, Nav, Chrome (`--bg-chrome`) |
| `--eddy-800` – `--eddy-900` | | Display-Flächen, hohe Kontraste (`--bg-display`) |

### Warm — Sand, Wood, Sunset

| Token | Hex | Verwendung |
|---|---|---|
| `--sand-50` | `#FBF7F1` | Onboarding-Background (`--bg-onboarding`) |
| `--sand-100` – `--sand-400` | | warme Tints, Cards in Onboarding-Kontext |
| `--wood-700` | `#6B4E2E` | warme dunkle Akzente, sehr sparsam |
| `--sunset-400` – `--sunset-600` | | **Akzent** — Call-to-Action, Highlight |

> **Regel zum Sunset-Akzent:** maximal **ein** Moment pro Screen. Beispiel: der „Jetzt starten"-Button auf der Landing-Page — sonst nirgends auf derselben Seite. Wird der Akzent inflationär, verliert er seine Funktion und das ruhige Gesamtbild kippt.

### Neutrals

Leicht warme Graustufen von `--neutral-0` (Weiß) bis `--neutral-900` (fast Schwarz). Verwende die **semantischen** Aliase, nicht die Skala direkt, sofern möglich — sie machen Refactoring trivial:

| Alias | Mapping | Verwendung |
|---|---|---|
| `--bg-app` | `--neutral-25` | App-Hintergrund |
| `--bg-surface` | `--neutral-0` | Karten, Modals, Forms |
| `--bg-tinted` | `--eddy-50` | leicht getönte Sektionen |
| `--bg-onboarding` | `--sand-50` | nur Onboarding |
| `--bg-chrome` | `--eddy-700` | Header / Nav |
| `--bg-display` | `--eddy-900` | öffentliche Anzeigen, hochkontrastige Display-Modi |
| `--fg-default` | `--neutral-800` | Standard-Text |
| `--fg-muted` | `--neutral-500` | sekundärer Text, Captions |
| `--fg-soft` | `--neutral-400` | Hinweise, Disabled |
| `--fg-on-chrome` | `--neutral-0` | Text auf dunklem Chrome |
| `--fg-link` | `--eddy-500` | Links |
| `--border-soft` | `--neutral-200` | dezente Trenner |
| `--border-strong` | `--neutral-300` | sichtbare Outlines |
| `--focus-ring` | primary @ 28% | Tastatur-Fokus, immer sichtbar |

### Semantik

| Token | Hex | Verwendung |
|---|---|---|
| `--signal` | `#2E7A9E` | Info, identisch mit Primary |
| `--success` | `#3F8A5C` | bestätigte Aktionen — Waldgrün, nicht Neon |
| `--warn` | `#C98A26` | warnen ohne zu alarmieren |
| `--danger` | `#9B2F3A` | destruktive Aktionen — Burgund, nicht Feuerrot |
| `--danger-600` | `#7E2530` | Hover/Pressed auf Danger |

### Group-Palette

`--group-1` … `--group-10` — 10 Farben für Gruppen-/Kategorie-Codierung (z.B. Boots-Gruppen in KEP, Tags in RDB). Alle sind so gewählt, dass **weißer Text mit WCAG AA (≥ 4.5:1) Kontrast** lesbar bleibt. Stabil in der Reihenfolge zuweisen, nicht nach Gefühl mischen, damit dieselbe Gruppe in verschiedenen Views dieselbe Farbe trägt.

## Typografie

**Schrift:** Nunito Sans — eine Schriftfamilie, alle Gewichte. Lokal eingebunden über zwei Variable Fonts (`fonts/NunitoSans-VariableFont.ttf` für Normal, `…-Italic-VariableFont.ttf` für Kursiv).

Fallback-Stack: `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif`.

### Skala (mobile-first)

| Token | Größe | Semantisch | Klasse |
|---|---|---|---|
| `--fs-caption` | 12px | Captions, Labels | `.eddy-caption`, `.eddy-label` |
| `--fs-small` | 14px | sekundärer Text | `.eddy-small` |
| `--fs-body` | 16px | Fließtext | `.eddy-body`, `.eddy-body-strong` |
| `--fs-lead` | 18px | Lead-Absatz | `.eddy-lead` |
| `--fs-h3` | 20px | H3 | `.eddy-h3` |
| `--fs-h2` | 24px | H2 | `.eddy-h2` |
| `--fs-h1` | 28px | H1 | `.eddy-h1` |
| `--fs-display` | 36px | Display | `.eddy-display` |
| `--fs-hero` | 48px | Hero / Landing | `.eddy-hero` |

### Klassen-Spielregeln

- **Display- und Hero-Klassen** (`.eddy-display`, `.eddy-hero`) sind absichtlich **weight 400** mit enger Laufweite (`--tr-display: -0.02em`) — schwerer wirkt zu prominent für den ruhigen Vibe.
- **Headings** (`.eddy-h1`, `.eddy-h2`) sind **700**, `.eddy-h3` ist **600** — strukturieren ohne zu schreien.
- **Labels** (`.eddy-label`) sind kleine, getrackte Caps (`--tr-label: 0.08em`) für Kennzeichnungen wie `KEHRWASSER`, `DO-1`. Immer in `--fg-muted`.
- **Tabular Numerals** über `.eddy-tabular` (oder direkt `.eddy-data` für Daten-Tabellen mit `font-weight: 600`). Pflicht, wenn Zahlen in Spalten ausgerichtet werden.

### Line-Height / Tracking

| Token | Wert | Verwendung |
|---|---|---|
| `--lh-tight` | 1.15 | Displays, große Headlines |
| `--lh-snug` | 1.30 | H2/H3 |
| `--lh-normal` | 1.50 | Fließtext (Default) |
| `--lh-relaxed` | 1.65 | längere Lesepassagen, Wiki-Content |
| `--tr-ui` | -0.015em | Default für UI-Text |
| `--tr-display` | -0.020em | Displays und Hero |
| `--tr-label` | 0.080em | nur für `.eddy-label` |

## Spacing & Radien (4px-Basis)

| Token | Wert | Verwendung |
|---|---|---|
| `--space-1` | 4px | feinste Abstände, Icon-Padding |
| `--space-2` | 8px | Inline-Gaps |
| `--space-3` | 12px | Card-Padding (mobil) |
| `--space-4` | 16px | **Page Gutter (mobil)** |
| `--space-5` | 20px | Section-Padding |
| `--space-6` | 24px | größere Trenner |
| `--space-7` | 32px | Section-Margin |
| `--space-8` | 40px | großzügige Trenner |
| `--space-9` | 56px | **Header-Höhe** |

`--hit-min: 44px` — minimale Treffer­fläche für interaktive Elemente. Buttons, Links, Toggles dürfen nie kleiner sein.

### Radien — semantisch nach Komponente

| Token | Wert | Komponente |
|---|---|---|
| `--radius-tag` | 4px | Tags, Chips |
| `--radius-control` | 10px | Buttons, Inputs, Selects |
| `--radius-list-card` | 14px | Listen-Karten |
| `--radius-tile` | 20px | Dashboard-Kacheln |
| `--radius-pill` | 999px | Pill-Buttons, Avatare |

Konsequenz: nie eigene Radius-Werte hardcoden — die Form der Komponente ergibt sich aus dem Token.

## Schatten

Fünf Stufen, alle **primary-dark getönt** (`rgba(20, 56, 72, α)`), nie pures Schwarz. Schatten signalisieren Höhe, nicht Dramatik.

| Token | Verwendung |
|---|---|
| `--shadow-xs` | dezente Trennung von Flächen |
| `--shadow-sm` | Listen-Karten |
| `--shadow-md` | schwebende Elemente (Dropdowns, kleine Modals) |
| `--shadow-lg` | Modale, Sheets |
| `--shadow-inset` | gedrückte Zustände, Wells |

## Motion

| Token | Wert | Verwendung |
|---|---|---|
| `--ease-out` | `cubic-bezier(0.22, 0.61, 0.36, 1)` | Element erscheint |
| `--ease-in` | `cubic-bezier(0.55, 0, 0.68, 0.53)` | Element verschwindet |
| `--ease-io` | `cubic-bezier(0.65, 0, 0.35, 1)` | symmetrische Übergänge |
| `--dur-fast` | 120ms | Hover, Fokus |
| `--dur-base` | 200ms | UI-Transitions |
| `--dur-page` | 250ms | Routenwechsel, Sheets |

Motion soll **bestätigen, nicht performen**. Wenn eine Animation auffällt, ist sie meist zu lang oder zu groß.

## Faustregeln

1. **Token statt Hex.** Wenn du `#2E7A9E` schreibst statt `var(--eddy-500)`, ist die Migration auf einen späteren Re-Brand teurer als nötig.
2. **Semantische Aliase bevorzugen.** `var(--fg-default)` statt `var(--neutral-800)` — der Alias bleibt, das Mapping kann sich ändern.
3. **Sunset sparsam.** Max ein Moment pro Screen.
4. **Schatten getönt.** Wenn ein Schatten schwarz wirkt, stimmt er nicht.
5. **Mindesttreffer 44px.** Paddler bedienen die App auch mit kalten oder nassen Fingern.
6. **`prefers-reduced-motion` respektieren.** Wenn JS-Motion dazukommt: erst prüfen, dann animieren.
7. **Eine Schrift, eine Familie.** Nunito Sans deckt alles ab. Keine zweite Schrift „für den Akzent".

## Erweiterung

Neue Tokens werden in `colors_and_type.css` ergänzt und hier dokumentiert. Reihenfolge: Token → README-Zeile → Verwendung im Code. Tokens ohne dokumentierte Verwendung sollen vermieden werden — sie laden zu Wildwuchs ein.

## Offen / zu klären

- `--bg-display` ist mit „public display / Teil 7" annotiert — Kontext (welche App, welcher Screen) noch nicht festgehalten.
- Dark-Mode-Strategie ist noch nicht definiert. Sobald sie kommt, werden die semantischen Aliase (`--bg-*`, `--fg-*`, `--border-*`) in einem `@media (prefers-color-scheme: dark)`-Block neu gemappt; die Skala bleibt unverändert.
