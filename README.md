# CSS Files for Decidim Awesome - Mitwirken an Zürichs Zukunft

This directory contains CSS files used with [Decidim Awesome](https://github.com/decidim-ice/decidim-module-decidim_awesome) on the Zürich Decidim installation **"Mitwirken an Zürichs Zukunft"** (https://mitwirken.stadt-zuerich.ch), based on the Decidim Zürich codebase **[`puzzle/decidim-zuerich`](https://github.com/puzzle/decidim-zuerich)**.

## Overview

These CSS files customize Decidim to match the [Stadt Zürich (STZH) design system](https://designsystem.stadt-zuerich.ch/current/?path=/docs/docs-about--docs): color palette, typography, spacing, and component patterns, plus extra rules needed for real participatory processes. Each file is included in its own box in Decidim Awesome and can be scoped per page, component, or space.

The sections **Design system (sources and deviations)** and **Breakpoints and horizontal padding** below describe how we apply STZH to Decidim—where we follow the official system, where we use Tailwind-style breakpoints for Decidim compatibility, and how layout width and padding behave across viewports.

## Design system: sources and deviations

### Sources

- **Reference:** [designsystem.stadt-zuerich.ch](https://designsystem.stadt-zuerich.ch/current/)
- **Package:** `@oiz/stzh-components` (via [jsDelivr CDN](https://cdn.jsdelivr.net/npm/@oiz/stzh-components@latest/))
- **Import chain:** `a1_variables.css` imports `stzh-components.css`; `b1_reskin_updated.css` loads after A1 and applies the reskin (see **File organization** for all sheets).

### Breakpoints

The STZH design system uses its own breakpoint scale:

| STZH breakpoint | Min-width | Typical use |
|-----------------|-----------|-------------|
| —               | (default) | Base styles |
| Medium          | **900px** | Layout and typography adjustments |
| Large           | **1260px**| Further scaling |

**Decidim / Mitwirken** follows **Tailwind CSS** breakpoints instead, for compatibility with Decidim’s grid and utilities:

| Our breakpoint | Min-width | Source |
|----------------|-----------|--------|
| (base)         | —         | Default |
| sm             | **640px** | Tailwind |
| md             | **768px** | Tailwind |
| lg             | **1024px**| Tailwind |
| xl             | **1280px**| Tailwind |
| 2xl            | **1536px**| Tailwind |

Typography and some components (e.g. help text, footer) still use **900px** and **1260px** where those values match the STZH spec.

### Other deviations

- **Borders:** `.rounded` is reset to `border-radius: 0` (STZH favours square corners).
- **Text:** `.text-center` and `.uppercase` are overridden to left-aligned and normal case where not needed.
- **Font loading:** Fonts come from `@oiz/stzh-components`; Decidim’s default font loading is replaced.
- **Flash messages:** The Banner pattern is adapted to Decidim’s markup (icon, message, close button) with a full-width background via `::before`, while the content box follows main layout alignment.

## Breakpoints and horizontal padding

Main layout uses responsive horizontal padding so content lines up across header, body, and footer. The same scale is used for flash messages, Devise pages, hero blocks, and similar areas.

### Reference scale (content box)

| Viewport        | Breakpoint | Max-width (content) | Horizontal padding |
|-----------------|------------|---------------------|--------------------|
| Under 640px     | (base)     | 100%                | `var(--stzh-space-medium)` |
| ≥ 640px         | sm         | 640px               | `var(--stzh-space-xlarge)` |
| ≥ 768px         | md         | 768px               | (unchanged) |
| ≥ 1024px        | lg         | 1024px              | `var(--stzh-layout-padding-desktop)` (4rem) |
| ≥ 1280px        | xl         | 1280px              | (unchanged) |
| ≥ 1536px        | 2xl        | 1536px              | (unchanged) |

### Where this applies

- **Flash messages** (`flash[role="alert"]`): Content box uses this max-width and padding; background stays full-width via `::before`.
- **Devise** (sign-in, registration, password, etc.): `.layout-main` uses `--stzh-space-medium` → `--stzh-space-xlarge` (from 640px) → `--stzh-space-xxlarge` (from 1024px).
- **Hero** (`.hero > *`): Uses `--stzh-space-xxlarge` on larger viewports.
- **Footer** (`.main-footer__down`): Uses `var(--stzh-layout-padding-desktop)` on large screens.
- **Process hero** (`.participatory-space__hero-text`): Uses `var(--stzh-layout-padding-desktop)` from 1024px+ and scales `max-width` by breakpoint.

### STZH spacing variables (padding)

| Variable                         | Approx. value | Typical use |
|----------------------------------|---------------|-------------|
| `--stzh-space-medium`            | ~1rem         | Base mobile padding |
| `--stzh-space-xlarge`            | ~2rem         | Tablet padding |
| `--stzh-space-xxlarge`           | ~2.5–3rem     | Desktop padding (some areas) |
| `--stzh-layout-padding-desktop`  | 4rem (64px)   | Desktop padding (layout-main, flash, footer, hero from 1024px+) |

### Max-width and padding together

1. **Max-width** caps the content box so line length stays readable on large screens.
2. **Padding** keeps content off the viewport edges on small screens and a consistent inset at each step.
3. Content is centred with `margin-left: auto; margin-right: auto` inside the padded area.
4. At each breakpoint, max-width matches the breakpoint width (640px, 768px, 1024px, …) so the box grows with the viewport up to that limit.

This aligns with Decidim’s `.home__section` and `.home .content-block` and with STZH where breakpoints allow.

## Naming convention

The file naming convention follows a hierarchy:

- **Class A** – Variable & theme sheets
- **Class B** – Reskins
- **Class C** – Functional and design adjustments
- **Class D** – Process-specific customizations

Each file uses its class prefix (lowercase letter), a number, and a descriptive name (e.g. `a1_variables.css`, `c3_forms.css`).

## File organization

### Class A – Variable & theme sheets

Foundation: CSS custom properties (variables).

| File | Box Name | Description |
|------|----------|-------------|
| `a1_variables.css` | A1 | Imports STZH variables from `stzh-components` and defines Decidim-specific token overrides |
| `a2_VBZ_variables.css` | A2 | VBZ (Verkehrsbetriebe Zürich) design tokens (enable only for VBZ-scoped content) |

### Class B – Reskins

Global application of the design system across the platform.

| File | Box Name | Description |
|------|----------|-------------|
| `b1_reskin_updated.css` | B1 | Main reskin: typography, buttons, cards, navigation, layouts |

**Note:** By naming, B2 would be VBZ reskin; VBZ-specific visual tweaks live in **`c2_VBZ_adjustments.css`** (Class C).

### Class C – Functional and design adjustments

| File | Box Name | Description |
|------|----------|-------------|
| `c1_functionalAdjustments.css` | C1 | Functional tweaks (hide elements, layout fixes) independent of the reskin |
| `c2_VBZ_adjustments.css` | C2 | VBZ-specific design adjustments |
| `c3_forms.css` | C3 | Form styling |
| `c4_mapSize.css` | C4 | Map size and layout |
| `c5_hideGeo.css` | C5 | Hide geo-related UI |
| `c6_hideProcesses.css` | C6 | Hide process-related UI |
| `c7_sharetokens.css` | C7 | Share-token styling |
| `c8_meetingAdjustments.css` | C8 | Meeting-related adjustments |
| `c9_ProcessGroupBannerWeiss.css` | C9 | Process group banner (white variant) |

### Class D – Process-specific customizations

| File | Box Name | Description |
|------|----------|-------------|
| `d1_fahrgaststimme.css` | D1 | “Fahrgaststimme” process |
| `d1a_nettoNullMeetings.css` | D1a | Netto Null meetings |
| `d2_proc-nettonull.css` | D2 | Netto Null process theme |
| `d3_proc_Quartierblöcke.css` | D3 | “Quartierblöcke” process |
| `d4_klimainstitutionen.css` | D4 | Climate institutions |
| `d5_archivierteProzesse.css` | D5 | Archived processes |

## Installation in Decidim Awesome

1. **Boxes:** Create one Decidim Awesome custom-styles box per CSS file.
2. **Names:** Use the box labels from the tables (A1, A2, B1, C1, …).
3. **Content:** Paste each file’s contents into the matching box.
4. **Scoping (optional):** Restrict boxes to specific pages, components, or participatory spaces.
5. **Order:** Load in cascade order:
   - Class A (variables first)
   - Class B (reskin)
   - Class C (adjustments)
   - Class D (process-specific last)

### Hiding from public frontend

To keep custom CSS available in admin but hidden on the public site, add a wrapper class and adjust the box’s `data-key` (or equivalent) in Decidim Awesome so visibility rules apply as needed.

## Additional notes

- **Dependencies:** Class A must load before everything else; later sheets depend on those custom properties.
- **VBZ:** Enable A2 / C2 only for VBZ-related scopes.
- **Class D:** Enable each D sheet only for its process.
- **Maintenance:** Keep naming and class structure when adding or changing files.

## Decidim versions and Git branches

Each Decidim major/minor line has its **own branch** with a **full set of CSS files** at the repo root (same names as in the tables above). You copy files from the branch that matches the backend you are editing—not from commit messages on a single shared tree.

| Decidim version | Branch | Use for |
|-----------------|--------|---------|
| **0.29** (current production) | `maint/decidim-0.29` | Live site, hotfixes |
| **0.31** (upgrade) | `upgrade/decidim-0.31` | Staging / new platform |
| Integration | `main` | Merged baseline; keep in sync when a version branch is promoted |

**Baseline tag:** `css/decidim-0.29-baseline` — snapshot when 0.29 and 0.31 branches were created (after merging `automation` into `main`).

### Copy-paste workflow

1. **One version at a time:** `git checkout maint/decidim-0.29` or `git checkout upgrade/decidim-0.31`, then open the `.css` files in this folder and paste into Decidim Awesome.
2. **Both versions at once (recommended):** use a second [git worktree](https://git-scm.com/docs/git-worktree) so two folders exist on disk, each on its branch:

```bash
cd "/Users/lars/kDrive/Common documents/Projekte/_DecidimZuerich/CSS/github"
git worktree add ../github-decidim-0.31 upgrade/decidim-0.31
```

- `github/` → stay on `maint/decidim-0.29` for 0.29 paste
- `github-decidim-0.31/` → `upgrade/decidim-0.31` for 0.31 paste

Commit on the branch that matches the instance you changed. Cherry-pick between branches when a fix applies to both markup versions.

### Pushing to GitHub

After review locally:

```bash
git push origin main
git push origin maint/decidim-0.29 upgrade/decidim-0.31
git push origin css/decidim-0.29-baseline
```

## Further reading

- [STZH design system](https://designsystem.stadt-zuerich.ch/current/)
- [Decidim documentation](https://docs.decidim.org/)
- [Tailwind CSS breakpoints](https://tailwindcss.com/docs/responsive-design)
- [Decidim Awesome](https://github.com/decidim-ice/decidim-module-decidim_awesome)
