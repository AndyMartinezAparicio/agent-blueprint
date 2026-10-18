---
name: material-design
description: "Trigger: design decision, visual hierarchy, card vs text vs list, emphasis, component choice, type scale, color roles, shape, states, Material 3. Apply Material 3 guidance to {{NOMBRE_PROYECTO}} before proposing options."
license: Apache-2.0
metadata:
  author: "AndyMAG"
  version: "1.1"
---

## Activation Contract

Use BEFORE proposing design options to the user: layout of a screen section, card vs plain text vs list item, emphasis, component choice, typography/color roles, shape, states, accessibility. Load `project-ui` too (and `flutter-build-responsive-layout` for layout).

## Precedence

1. `docs/` decides WHAT exists (AGENTS.md rules 1-3). Never add features, texts or buttons not in `docs/`.
2. `design/DESIGN.md` "Notas del proyecto" and `project-ui` beat this skill on anything visual.
3. This skill = generic Material 3 guidance, only where 1-2 are silent.

## Hard Rules

- Map every decision to theme roles, never literals: `colorScheme`, `context.{{CLASE_COLORES}}` (`app_palette.dart`), `textTheme`, `AppSpacing`, `AppRadii` (see `project-ui`).
- Build hierarchy with the type scale and color roles first; add containers (cards) only when they earn their place.
- Touch targets >= 48x48 dp; never convey meaning by color alone (pair with text/icon).
- One primary emphasis per section; strong colors keep their semantic meaning.
- Cite only rules in `references/` (`material-3.md`, `components.md`, `theming.md`). If a rule is not there, say it is project judgment, not Material.

## Decision Gates

| Need | Use (Flutter) |
|------|---------------|
| Informational summary, no action | Plain text with type-scale hierarchy (`displaySmall`/`headlineSmall` number + `bodyMedium`/`labelMedium` caption) on `surface`; no card |
| Distinct unit, grouped or tappable content | `Card.filled` (default for {{NOMBRE_PROYECTO}}) or `Card.outlined`; `Card` elevated only if it must float |
| Simple row: text + leading/trailing | `ListTile` (1-3 lines); custom `Row` if it does not fit |
| Highest-emphasis action | `FilledButton` (or FAB); mid `FilledButton.tonal`; low `TextButton` |
| Separate regions without a container | Spacing first (4/8 grid), then `outlineVariant`/`hairline` divider |
| Less-emphasis accent | `primaryContainer` / `secondary`; `tertiary` only to draw attention |
| Content on a color | Always its `on*` pair |
| Toggle/filter a set of options | `FilterChip` / `ChoiceChip` in a `Wrap` (chips are a compact alternative to checkboxes) - `components.md` Chips |
| Brief feedback or undo after an action | `SnackBar` with one `SnackBarAction`; not a dialog - `components.md` Snackbar |
| Interrupt for a decision / confirmation | `AlertDialog`, sparingly; choices without interruption go in `showModalBottomSheet` - `components.md` Dialogs, Bottom sheets |
| Unknown vs known wait | Indeterminate vs determinate `LinearProgressIndicator`; one type per activity - `components.md` Progress |
| Section separation | Full-width divider for unrelated sections, inset for related items - `components.md` Divider |
| Motion timing/easing | `theming.md` Motion table; duration grows with distance |

Type roles: display = hero numbers; headline = section/screen titles; title = card/list titles; body = reading text; label = buttons, chips, captions.

## Execution Steps

1. Load `project-ui` + this skill; read `references/material-3.md` for the section you need.
2. Check `docs/` and DESIGN.md "Notas del proyecto" for constraints.
3. Draft at most 2-3 options, each with an ASCII preview and the rule that backs it.
4. Recommend one; include a brief quality note (usability, accessibility, performance) per AGENTS.md rule 8.
5. Wait for approval before coding.

## Output Contract

Per option: ASCII preview, widgets/roles used, backing rule (`project-ui`, `material-design` section, or DESIGN.md), cost. End with a recommendation.

## References

- `references/material-3.md` - color roles, type scale, shape/elevation, cards, lists, buttons, a11y basics, with source URLs.
- `references/components.md` - buttons, FAB, cards, lists, chips, top app bar, bottom sheets, dialogs, snackbar, progress, tabs, drawer, divider (from material-components-android docs, mapped to Flutter).
- `references/theming.md` - color, typography, shape, motion theming (same source).

Not covered: state layers, layout/window size classes, text fields, menus, switches/sliders, navigation bar specs, m3.material.io prose (page is JS-rendered, not fetchable). Mark anything outside the references as project judgment.
