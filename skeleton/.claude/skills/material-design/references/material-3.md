# Material 3 reference for {{NOMBRE_PROYECTO}}

Only claims actually read from the fetched sources appear under "Source". Lines marked "Project judgment" are not official Material text.

## Fetch status

- FAILED (page is JS-rendered, only the title came back): m3.material.io `components/cards/guidelines`, `styles/typography/type-scale-tokens`, `styles/color/roles`, `components/lists/guidelines`, `foundations/designing/structure`. `foundations/accessible-design/accessibility-basics` returned 404. No rules are taken from them. Open them in a browser if you need the official prose (when to use cards, list anatomy, spacing).
- OK: api.flutter.dev (Card, ColorScheme, TextTheme, ListTile), developer.android.com Compose Material 3, raw material-web docs (color, typography).
- Partial: docs.flutter.dev/ui/design/material (no useful content); developer.android.com Compose accessibility overview (no details).

## Color roles
Source: https://api.flutter.dev/flutter/material/ColorScheme-class.html, https://developer.android.com/develop/ui/compose/designsystems/material3

- `primary`: most frequent accent (FAB, prominent buttons, active states). `onPrimary` on top.
- `primaryContainer`: elements needing less emphasis than `primary`.
- `secondary`: less prominent components (e.g. filter chips). `tertiary`: contrasting accent that balances or draws attention.
- `error`: validation errors.
- `surface` background; `onSurface` content. `surfaceContainerLowest` < `Low` < `surfaceContainer` < `High` < `Highest` = increasing emphasis against `surface`.
- `outline`: boundaries/emphasis; `outlineVariant`: decorative boundaries such as dividers (3:1 contrast not required).
- Always place `onX` on `X`; never mix containers with another role's content (poor contrast).
- Emphasis comes from surface tones with `onSurface` / `onSurfaceVariant`.

## Typography
Source: https://api.flutter.dev/flutter/material/TextTheme-class.html, https://developer.android.com/develop/ui/compose/designsystems/material3

5 roles x 3 sizes (size/line height): displayLarge 57/64, displayMedium 45/52, displaySmall 36/44; headlineLarge 32/40, Medium 28/36, Small 24/32; titleLarge 22/28, titleMedium 16/24 (w500), titleSmall 14/20 (w500); bodyLarge 16/24, bodyMedium 14/20, bodySmall 12/16; labelLarge 14/20 (w500), labelMedium 12/16 (w500), labelSmall 11/16 (w500).
Flutter: `Theme.of(context).textTheme.<style>`. {{NOMBRE_PROYECTO}} builds its own scale in `app_typography.dart`; use only its styles.
Project judgment: role-to-usage mapping in SKILL.md (display=hero number, label=captions).

## Shape and elevation
Source: https://developer.android.com/develop/ui/compose/designsystems/material3

- Shape scale: extraSmall, small, medium, large, extraLarge (Reply sample 4/8/12/16/24 dp); also rectangle and fully rounded.
- M3 elevation is mainly tonal (surface color overlay) plus optional shadow. In {{NOMBRE_PROYECTO}} use surface tones (`surface1`/`surface2` in `app_palette.dart`) instead of shadows (project judgment).

## Cards
Source: https://api.flutter.dev/flutter/material/Card-class.html

- Three M3 variants: `Card` (elevated, rounded corners + shadow), `Card.filled`, `Card.outlined`. All share `CardThemeData` (e.g. `shape`).
- The official source gives no criteria for choosing between variants or when not to use a card.
- Project judgment: use a card for a distinct, tappable or groupable unit; use plain text for a read-only summary. Avoid nesting cards.

## Lists
Source: https://api.flutter.dev/flutter/material/ListTile-class.html

- `ListTile`: fixed-height row, 1 line (`title`), 2 (`subtitle`), 3 (`isThreeLine`). Title must not wrap; subtitle at most 2 lines when three-line.
- `leading`/`trailing` should respect the Material spec; one-line tiles allow tappable targets of at least 48x48. Constrain widths yourself.
- Needs a `Material` ancestor (Scaffold). If the layout does not fit, build a custom item with `Row`/`Column`/`Expanded`.

## Buttons and navigation
Source: https://developer.android.com/develop/ui/compose/designsystems/material3

- Emphasis order: extended FAB (highest) > filled button (high) > text button (low). Flutter: `FloatingActionButton.extended`, `FilledButton`, `FilledButton.tonal`, `TextButton`.
- `NavigationBar`: compact screens, up to 5 destinations.

## Accessibility
Source: https://api.flutter.dev/flutter/material/ListTile-class.html (48x48 targets); https://developer.android.com/develop/ui/compose/designsystems/material3 (on-X contrast pairing).

- Touch targets >= 48x48 dp; contrast via correct `on*` pairs.
- Official pages for contrast ratios, text scaling and labels were not fetched. Project rules for them live in `project-ui` (Semantics labels, large font scale).

## Not covered
Now covered in `components.md` and `theming.md`: chips, FAB, top app bar, bottom sheets, dialogs, snackbar, progress indicators, tabs, drawer, divider, motion.
Still not covered: state layers, layout/window size classes, text fields, menus, switches/sliders, exact navigation bar specs. Do not cite Material for these; use `project-ui` / `design/DESIGN.md` or flag as project judgment.
