# DARK-VIBE for Mailspring

DARK-VIBE is a dark UI theme for Mailspring built as a small, coherent design
system: cool neutral surfaces, a single vibrant blue accent, calm contrast and
consistent interaction states across the whole app.

## Visual direction

- **Surfaces, not borders** — navigation, content and floating layers sit on a
  short ladder of dark greys (~2% luminance per step). Hairlines are white at
  6–14% opacity and only appear where a surface needs an edge.
- **One accent, two roles** — `#64b5f6` for text, icons, outlines and tints on
  dark surfaces; a deeper `#1b6fd0` for solid fills that carry white text
  (primary buttons, selected menu items, selected tokens, notifications).
- **Restrained states** — hover is a 5% white overlay, pressed 9%, selection an
  accent tint. The opened thread gets a 4px accent bar and a soft tint with a
  short glow from the bar; nothing else moves or lifts.
- **Typography** — Mailspring's bundled `Nylas-Pro` with system fallbacks,
  18px semibold thread subject, 11px uppercase section labels, tabular
  numerals for counters and timestamps.
- **Motion** — 110–160ms colour transitions on controls only; list rows are
  instant.

## Design tokens

Defined once in `styles/ui-variables.less` (prefix `dv-`), then mapped onto
Mailspring's own variables so every core stylesheet picks them up.

| Group      | Tokens                                                                                   |
| ---------- | ---------------------------------------------------------------------------------------- |
| Surfaces   | `n-900` sidebar · `n-850` lists, reading pane, toolbars · `n-800` unread rows, bars · `n-750` cards, composer · `n-700` buttons, menus, popovers · `n-650` / `n-600` hover / pressed |
| Accent     | `accent`, `accent-strong`, `accent-fill`, `accent-fill-hover/active`, `on-accent`, `on-accent-light` |
| Semantic   | `success`, `warning`, `danger`, `reminder`                                               |
| Text       | `text`, `text-strong`, `text-secondary` (72%), `text-muted` (50%), `text-faint` (36%)    |
| Lines      | `line-subtle` (6%), `line` (9%), `line-strong` (14%)                                     |
| Overlays   | `hover` (5%), `active` (9%), `accent-tint` (12%), `accent-tint-strong` (20%)             |
| Shape      | `radius-sm` 4px · `radius` 6px · `radius-lg` 8px · `radius-pill`                         |
| Elevation  | `shadow-1/2/3`, `ring` (hairline for floating surfaces), `focus-ring`, `btn-shadow`, `fill-shadow` |
| Motion     | `ease`, `fast` 110ms, `normal` 160ms                                                     |

## Project structure

- `styles/ui-variables.less` — tokens and Mailspring variable overrides.
  Mailspring imports this file into every core stylesheet and into the theme
  picker preview, so it must contain **variables only**.
- `styles/index.less` — the component layer, organised by area: foundations,
  layout, navigation, thread list, reading pane, composer, controls,
  preferences and modals, blurred window, bundled plugins. Selectors mirror the
  core ones so the theme wins ties without `!important` (used only where core
  itself relies on `!important` or inline styles).

## Technical notes

- Targets Mailspring 1.22+; no dependencies, no remote resources, no runtime
  code. Only Mailspring's LESS pipeline is used.
- Class names, layout metrics and the `index.less` entry point are the ones
  Mailspring expects; nothing functional is renamed or removed.
- The email body is rendered in an iframe that only receives Mailspring's own
  `email-frame.less` compiled with this theme's variables (text, link and
  highlight colours). HTML emails keep their own backgrounds on purpose — no
  inversion filter is applied.
- Native form controls opt into the dark colour scheme individually. The
  document root deliberately stays in the normal scheme: an inherited dark
  scheme makes Chromium paint an opaque white backdrop behind light-scheme
  iframes, which would hide the text of plain emails.
- The accent is fixed by the theme and does not mirror the OS accent colour.

## Installation

1. Clone this repository:

```bash
git clone https://github.com/Sud0ck3rs/DARK-VIBE.git
```

2. Open Mailspring and go to `Edit` -> `Install Theme...`
3. Select the downloaded `dark-vibe` folder
4. Restart Mailspring if the theme is not applied instantly

## Compatibility

- Mailspring: `*` (see `package.json`), designed against 1.22
- Theme type: `ui`
