# CSS Files for Decidim Awesome - Mitwirken an Zürichs Zukunft

This directory contains CSS files used with [Decidim Awesome](https://github.com/decidim-ice/decidim-module-decidim_awesome) on the [Decidim installation](https://github.com/decidim/decidim) of Zürich: **"Mitwirken an Zürichs Zukunft"** (https://mitwirken.stadt-zuerich.ch).

## Overview

These CSS files customize the Decidim platform to match the Stadt Zürich (STZH) design system. Each file must be included in a separate box in Decidim Awesome and can be scoped accordingly.

## Naming Convention

The file naming convention follows a hierarchical structure:

- **Class A** – Variable & theme sheets
- **Class B** – Reskins
- **Class C** – Functional and design adjustments
- **Class D** – Process-specific customizations

Each file is named with its class prefix (lowercase letter) followed by a number and a descriptive name (e.g., `a1_variables.css`, `c3_forms.css`).

## File Organization

### Class A – Variable & Theme Sheets

These files define CSS custom properties (variables) that form the foundation of the design system.

| File | Box Name | Description |
|------|----------|-------------|
| `a1_variables.css` | A1 | Global STZH (Stadt Zürich) variables - defines color palette, typography, spacing, and other design tokens |
| `a2_VBZ_variables.css` | A2 | VBZ (Verkehrsbetriebe Zürich) specific variables |

### Class B – Reskins

These files contain global reskinning styles that apply the design system to the platform.

| File | Box Name | Description |
|------|----------|-------------|
| `b1_reskin_updated.css` | B1 | Global reskin - applies STZH design system styles across the platform (typography, buttons, cards, navigation, etc.) |

**Note:** According to the convention, B2 would contain VBZ adjustments, but this file is currently implemented as `c2_VBZ_adjustments.css` in Class C.

### Class C – Functional and Design Adjustments

These files contain specific functional adjustments, component customizations, and feature-specific styles.

| File | Box Name | Description |
|------|----------|-------------|
| `c1_functionalAdjustments.css` | C1 | Functional adjustments independent of reskinning (hides elements, fixes layout issues) |
| `c2_VBZ_adjustments.css` | C2 | VBZ-specific design adjustments |
| `c3_forms.css` | C3 | Form styling customizations |
| `c4_mapSize.css` | C4 | Map size and layout adjustments |
| `c5_hideGeo.css` | C5 | Hides geographic/geo features |
| `c6_hideProcesses.css` | C6 | Hides process-related elements |
| `c7_sharetokens.css` | C7 | Share token styling |
| `c8_meetingAdjustments.css` | C8 | Meeting-related adjustments |
| `c9_ProcessGroupBannerWeiss.css` | C9 | Process group banner styling (white variant) |

### Class D – Process-Specific Customizations

These files contain styles specific to individual participatory processes or initiatives.

| File | Box Name | Description |
|------|----------|-------------|
| `d1_fahrgaststimme.css` | D1 | Customizations for the "Fahrgaststimme" process |
| `d1a_nettoNullMeetings.css` | D1a | Netto Null meetings customizations |
| `d2_proc-nettonull.css` | D2 | Netto Null process theme variables and styling |
| `d3_proc_Quartierblöcke.css` | D3 | "Quartierblöcke" process customizations |
| `d4_klimainstitutionen.css` | D4 | Climate institutions customizations |
| `d5_archivierteProzesse.css` | D5 | Archived processes customizations |

## Installation in Decidim Awesome

### Setup Instructions

1. **Create CSS Boxes in Decidim Awesome**: For each CSS file, create a separate box in the Decidim Awesome custom styles interface.

2. **Box Naming**: Name each box using the provided convention (e.g., "A1", "A2", "B1", "C1", etc.) as shown in the table above.

3. **File Upload/Content**: Copy the contents of each CSS file into its corresponding box.

4. **Scoping (Optional)**: Each box can be scoped to specific pages, components, or participatory spaces if needed. Use Decidim Awesome's scoping options to limit where styles are applied.

5. **Loading Order**: The files should be loaded in the following order to ensure proper cascade:
   - First: Class A files (A1, A2) - variables must load first
   - Second: Class B files (B1) - reskins depend on variables
   - Third: Class C files (C1-C9) - adjustments depend on reskins
   - Fourth: Class D files (D1-D5) - process-specific styles depend on all above

### Hiding from Public Frontend

To hide custom styles from the public frontend while keeping them accessible in the admin interface:

- Add a new CSS class wrapper and replace the `data-key` attribute with the desired box name
- This allows selective visibility control through Decidim Awesome's interface

## Additional Notes

- **Dependencies**: Class A files (variables) must be loaded before all other files, as they define CSS custom properties used throughout.
- **VBZ**: Some files are specifically for VBZ (Verkehrsbetriebe Zürich) customizations and should only be enabled when working with VBZ-related content.
- **Process-Specific Files**: Class D files are scoped to specific participatory processes. Ensure they are only active for their respective processes.
- **Maintenance**: When updating styles, maintain the naming convention and class structure to ensure compatibility and easy identification.

## Design System Reference

These CSS files implement the **[Stadt Zürich (STZH) Design System](https://designsystem.stadt-zuerich.ch/current/?path=/docs/docs-about--docs)**, which includes:
- Comprehensive color palette (primary, secondary, semantic colors)
- Typography system with custom font families
- Spacing and layout variables
- Component styling guidelines

…plus additional requirements in the application of Decidim in real-world participatory processes.

For more information about the STZH Design System, refer to the official documentation.
