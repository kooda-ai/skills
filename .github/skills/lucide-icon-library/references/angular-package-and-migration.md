# Angular Package And Migration

Use this file for `@lucide/angular` or migration from `lucide-angular`.

## Package Surface
- The docs show installation for `@lucide/angular`.
- The docs show standalone per-icon usage such as importing `LucideFileText` and rendering `<svg lucideFileText></svg>`.
- The docs show direct icon inputs such as `size`, `color`, `strokeWidth`, `absoluteStrokeWidth`, and `title`.

## Dynamic And Name-Based Rendering
- `LucideIcon` is documented for dynamic rendering with imported icon components.
- The docs show dynamic tree-shaken rendering by passing imported icon components to `[lucideIcon]`.
- `provideLucideIcons(...)` is documented for registering icons by name for `lucideIcon="..."` usage.
- `LucideDynamicIcon` is shown in examples that render icons from signals or computed values.

## Global Defaults And Styling
- `provideLucideConfig(...)` is documented for global defaults such as `strokeWidth` or `size`.
- The docs show CSS styling on SVG elements and global `.lucide` styling.
- The docs also show a CSS pattern with `.lucide * { vector-effect: non-scaling-stroke; }` for absolute stroke behavior.

## Lucide Lab And Custom Angular Icons
- The docs show passing Lab icons directly as `LucideIconData`.
- The docs show name-based Lab icon registration through `provideLucideIcons(lucideLegacyIcon(...))`.
- The docs show custom standalone icon components built with:
  - `LucideIconBase`
  - `lucideIconTemplate`
  - `lucideLegacyIcon`
- The selector pattern shown in the docs is `svg[lucide{IconName}]`.

## Type And Validation Surface
- The docs show `LucideIconData` and `LucideIcon` type surfaces.
- The docs show `isLucideIconData()` and `isLucideIconComponent()` type guards.

## Migration Notes From `lucide-angular`
- The docs map `LucideAngularModule` to: static removed, dynamic `LucideIcon`.
- The docs map `LucideAngularModule.pick(...)` to `provideLucideIcons(...)`.
- The docs map `<lucide-angular name="foo-bar">` to `<svg lucideFooBar>`.
- The docs map `<lucide-icon [name]="expr">` to `<svg [lucideIcon]="expr">`.
- The docs map `<lucide-icon [img]="expr">` to `<svg [lucideIcon]="expr">`.
- The docs map `LucideIconConfig` to `provideLucideConfig(...)`.

## Angular-Specific Review Guardrails
- Distinguish between tree-shaken imported component usage and name-based provider usage.
- Keep `LucideDynamicIcon`, `LucideIcon`, `provideLucideIcons`, and `provideLucideConfig` separate in explanations.
- Preserve Angular template syntax exactly as documented when discussing migration or custom icons.
