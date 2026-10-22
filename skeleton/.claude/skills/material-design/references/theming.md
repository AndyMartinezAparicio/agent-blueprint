# Material 3 theming guidance (from material-components-android docs)

Base URL for every "Source": `https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/<File>.md`.
Flutter maps are project judgment. {{NOMBRE_PROYECTO}}'s own theme (`project-ui` / `DESIGN.md`) wins; use this only to justify choices.

## Color
Source: .../theming/Color.md
- Three accent groups (Primary, Secondary, Tertiary), each with 4-5 roles, plus non-brand roles (surface, outline, error...) that "ensure accessible color combinations".
- Components read theme color roles; change the theme, not each widget.
- Surfaces: M3 components use tonal surface color roles (surface container levels) instead of elevation overlays blended with primary; elevation overlay maintenance is discontinued.
- Default accents are purple when dynamic color is unavailable. Dynamic color (Android 12+) derives from the wallpaper and is applied as theme overlays.
- Custom colors: if you change one role, change its related roles to keep contrast. Keep the same luminance (tone) as the default role (e.g. primary tone 40 in light) to avoid breaking contrast.
- Name custom colors by hue/value, not by the role slot name.
- Flutter map: `ColorScheme` (`primary`, `primaryContainer`, `surfaceContainer*`, `outline`, `outlineVariant`); `dynamic_color` only if `docs/` adds it.

## Typography
Source: .../theming/Typography.md
- A set of type scales used throughout the app; components reference themeable text attributes.
- Baseline scale plus an emphasized scale: emphasized styles create hierarchy and are recommended for showing selection, actions, headlines or editorial treatments.
- A style = font face and weight, size, letter spacing, text transformation.
- Role/size table is in `references/material-3.md` (Typography).
- Flutter map: `TextTheme` via `Theme.of(context).textTheme`; emphasized = heavier `fontWeight` on the same role (project judgment).

## Shape
Source: .../theming/Shape.md
- Shape is a brand-expression dimension: corner family (rounded or cut) plus a corner-size scale.
- Scale: None 0dp, ExtraSmall 4dp, Small 8dp, Medium 12dp, Large 16dp, LargeIncreased 20dp, ExtraLarge 28dp, ExtraLargeIncreased 32dp, ExtraExtraLarge 48dp, Full 50% (circle/pill).
- The theme must keep sizes ordered (medium smaller than large); there is no automatic check.
- Override per component with an overlay instead of redefining theme-level values.
- Flutter map: `RoundedRectangleBorder` / `StadiumBorder` with {{NOMBRE_PROYECTO}}'s `AppRadii` in `project-ui` (use only its values; project judgment).

## Motion
Source: .../theming/Motion.md
- Easing + duration (curves) and springs as theme-level slots so animations feel cohesive. Duration grows with the area or distance traveled.
- Durations: short 50/100/150/200 ms, medium 250/300/350/400 ms, long 450/500/550/600 ms, extra-long 700/800/900/1000 ms.
- Easing: standard cubic-bezier(0.2, 0, 0, 1) for on-screen utility motion; standard decelerate (0, 0, 0, 1) entering; standard accelerate (0.3, 0, 1, 1) exiting; emphasized decelerate (0.05, 0.7, 0.1, 1) entering; emphasized accelerate (0.3, 0, 0.8, 0.15) exiting; linear for simple non-stylized motion.
- Springs: speed (fast for small components like switches, slow for full-screen, default otherwise) x type (spatial for movement, effects for color/opacity, which must not overshoot).
- Transition patterns: container transform (element with a container to its detail: card, list item, FAB), shared axis (forward/backward), fade through (top level), fade (enter/exit).
- Flutter map: `Curves.easeInOutCubicEmphasized`, `Curves.easeOutCubic`, `Duration(milliseconds: ...)` from the table; the `animations` package for container transform/shared axis would be a new package (needs ADR and approval per AGENTS.md).
- Respect the system "remove animations" setting (project judgment, accessibility).
