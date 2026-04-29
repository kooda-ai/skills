# Framework Components And Styling

Use this file for React, Preact, Solid, Vue, Svelte, Astro, or React Native component usage.

## Shared Patterns Confirmed Across Package Docs
- Framework packages document icons as inline SVG components.
- Multiple package pages recommend importing only the icons you need for tree-shaking.
- Multiple docs show `currentColor` as the default color behavior, so parent text color can style the icon.
- Multiple docs show prop-driven styling with `size`, `color`, `strokeWidth`, and `absoluteStrokeWidth`, but the exact prop names and casing must match the target package docs.
- Multiple docs show CSS sizing with `width` and `height` classes.
- Multiple docs show Tailwind `size-*` utility usage when Tailwind is configured.

## Direct Icon Imports Confirmed In Docs
- Astro docs show direct imports such as `@lucide/astro/icons/circle-alert`.
- Svelte docs show direct imports such as `@lucide/svelte/icons/camera` and `@lucide/svelte/icons/circle-alert`.
- Solid docs show direct imports such as `lucide-solid/icons/camera`.

## Global Default Props
- React docs show `LucideProvider` for global icon props.
- Preact docs show `LucideProvider` for global icon props.
- Solid docs show `LucideProvider` for global icon props.
- React Native docs show `LucideProvider` for global icon props.
- Vue docs show `setLucideProps` for global defaults.
- Svelte docs show `setLucideProps` for global defaults.

## Global CSS Patterns
- Multiple framework docs show `.lucide` CSS for global color, width, height, and stroke width.
- Multiple framework docs show `.lucide * { vector-effect: non-scaling-stroke; }` for global absolute stroke width behavior.

## Aliased Import Names
- React docs show `House`, `HouseIcon`, and `LucideHouse` as equivalent names.
- Preact docs show `House`, `HouseIcon`, and `LucideHouse` as equivalent names.
- Solid docs show `House`, `HouseIcon`, and `LucideHouse` as equivalent names.
- React Native docs show `House`, `HouseIcon`, and `LucideHouse` as equivalent names.

## Package-Specific Type Surfaces Mentioned In Docs
- React docs show `LucideProps`, `LucideIcon`, and `IconNode`.
- Preact docs show `LucideProps`, `LucideIcon`, and `IconNode`.
- Solid docs show `LucideProps`, `LucideIcon`, and `IconNode`.
- React Native docs show `LucideProps`, `LucideIcon`, and `IconNode`.
- Astro docs show `IconProps`, `LucideIcon`, and `IconNode`.
- Svelte docs show `LucideProps`, `LucideIcon`, and `IconNode`.
- Vue docs show `LucideProps` and `LucideIcon`.
- Use the package page for the exact type definition before quoting signatures.

## Filled Icons And Composition
- React docs show filled star examples using `fill` with `strokeWidth={0}`.
- Preact docs show filled star examples using `fill` with `strokeWidth={0}`.
- Solid docs show filled star examples using `fill` with `strokeWidth={0}`.
- Svelte docs show filled star examples using `fill` with `strokeWidth="0"`.
- React Native docs show filled icon examples and explicitly say fills are not officially supported but can work on specific icons.

## Framework Boundaries
- If the task is Angular-specific, switch to [angular-package-and-migration.md](./angular-package-and-migration.md).
- If the task is about raw SVG strings or builder output, switch to [core-web-static-and-builders.md](./core-web-static-and-builders.md).
