---
name: filament-5-styling
description: 'Use when: working with Filament 5 Styling, panel colors(), Color palettes, font(), Bunny Fonts, GoogleFontProvider, LocalFontProvider, custom themes, make:filament-theme, viteTheme(), Tailwind @source directives, darkMode(false), defaultThemeMode(), brandName(), brandLogo(), darkModeBrandLogo(), brandLogoHeight(), favicon(), maxContentWidth(), simplePageMaxContentWidth(), CSS hooks, FilamentAsset CSS registration, and panel styling assets. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Styling task, panel theme, branding/logo, dark mode, CSS hook, custom theme, asset registration, or code to review'
---

# Filament 5 Styling

## Purpose
Use this skill to create, review, or explain Filament 5 Styling using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Styling topic.
2. Do not add behavior, APIs, options, namespaces, commands, Tailwind behavior, asset behavior, CSS hook behavior, or conventions unless they appear in the retrieved documentation.
3. If a requested Styling topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Styling tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, command names, enum names, argument names, file paths, and CSS directives.

## Reference Map
- Colors, fonts, custom theme generation, Vite theme registration, Tailwind `@source`, dark mode, and default theme mode: [theme-basics.md](./references/theme-basics.md)
- Brand name, logos, favicon, maximum content width, and simple page width: [branding-layout.md](./references/branding-layout.md)
- CSS hook classes, CSS overrides, Blade-view warning, CSS asset registration, panel assets, CSS variables, lazy-loaded CSS, URL CSS assets, and plugin Tailwind guidance: [css-hooks-assets.md](./references/css-hooks-assets.md)

## Workflow
1. Identify the styling surface: panel colors, fonts, custom theme, Tailwind classes in app code, dark mode, default theme mode, branding, favicon, content width, CSS hooks, CSS assets, CSS variables, lazy-loaded CSS, or plugin styling guidance.
2. Run a narrow Context7 query for the exact styling topic before producing code.
3. Load the relevant reference file from the map above.
4. For panel styling code, use only documented `Panel` methods confirmed for the task, such as `colors()`, `font()`, `viteTheme()`, `darkMode(false)`, `defaultThemeMode()`, `brandName()`, `brandLogo()`, `darkModeBrandLogo()`, `brandLogoHeight()`, `favicon()`, `maxContentWidth()`, `simplePageMaxContentWidth()`, and `assets()`.
5. For colors, keep to documented semantic color keys, documented `Filament\Support\Colors\Color` palettes, documented hex or RGB generation, or documented OKLCH palette arrays.
6. For fonts, distinguish the documented default font, Google Fonts availability, Bunny Fonts default provider, `GoogleFontProvider`, and `LocalFontProvider` only when the current lookup confirms them.
7. For custom themes, include the documented `php artisan make:filament-theme` command, optional panel name, `--pm` option, generated CSS path pattern, manual Vite input, `viteTheme()` registration, `npm run build`, and Tailwind `@source` requirements only when confirmed.
8. For Tailwind utility classes in user Blade views, Livewire components, or PHP files, state the documented requirement for a custom theme before suggesting classes or `@apply` usage.
9. For dark mode, use only documented `darkMode(false)` and `defaultThemeMode(ThemeMode::Light|ThemeMode::Dark)` behavior confirmed by the lookup.
10. For branding, use only documented `brandName()`, `brandLogo()` with URL or HTML view callback, `darkModeBrandLogo()`, `brandLogoHeight()`, and `favicon()` patterns confirmed by the lookup.
11. For layout width, use only documented `Filament\Support\Enums\Width`, `maxContentWidth()`, `simplePageMaxContentWidth()`, documented defaults, and documented enum options confirmed by the lookup.
12. For CSS hooks, use documented `fi-` hook-class discovery, examples such as `.fi-sidebar`, documented `@apply` forms, documented `!important` guidance, and documented abbreviations. Do not invent hook class names.
13. For CSS assets, distinguish panel-specific `assets()` registration from global `FilamentAsset::register()` registration, and include `php artisan filament:assets`, `Css::make()`, `loadedOnRequest()`, `x-load-css`, `getStyleHref()`, URL CSS assets, and `registerCssVariables()` only when confirmed.
14. Finish by checking that every command, method, class, enum, argument, path, CSS directive, hook class, and code example in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Panel styling is configured in a panel provider method that accepts and returns `Filament\Panel`.
- Filament ships with 6 predefined semantic colors used throughout the framework: `danger`, `gray`, `info`, `primary`, `success`, and `warning`.
- `Filament\Support\Colors\Color` contains color options for Tailwind CSS color palettes.
- The docs confirm color generation from a singular hex value or RGB value, and custom palettes as arrays of OKLCH colors.
- The default font is Inter; `font('Poppins')` changes the panel font.
- Bunny Fonts CDN is used to serve fonts by default; the docs also confirm `Filament\FontProviders\GoogleFontProvider` and `Filament\FontProviders\LocalFontProvider`.
- A custom theme is created with `php artisan make:filament-theme`; multiple panels can pass a panel name, and the docs confirm `--pm` for a different package manager.
- A custom theme is required for Tailwind CSS classes in custom Blade views, Livewire components, or PHP files.
- The documented generated theme CSS includes `@source '../../../../app/Filament/**/*';` and `@source '../../../../resources/views/filament/**/*';`.
- Dark mode switching can be disabled with `darkMode(false)`.
- The default theme mode can be forced with `defaultThemeMode(ThemeMode::Light)` or `defaultThemeMode(ThemeMode::Dark)` using `Filament\Enums\ThemeMode`.
- Branding is documented with `brandName()`, `brandLogo()`, `darkModeBrandLogo()`, `brandLogoHeight()`, and `favicon()`.
- Panel content width is documented with `maxContentWidth()` and `simplePageMaxContentWidth()` using `Filament\Support\Enums\Width`.
- CSS hook classes are prefixed with `fi-`; the docs recommend discovering them with browser developer tools.
- The docs recommend CSS hook classes wherever possible instead of publishing internal Blade views.
- CSS assets can be registered globally with `FilamentAsset::register()` and `Css::make()`, or panel-specifically with `assets()` in panel configuration.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each method, class, enum, command, path, CSS directive, hook class, asset helper, argument, and code example is traceable to retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Tailwind habits, Laravel habits, package source code, or memory.
- If the user asks for a Styling topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, enum names, argument names, command flags, CSS selectors, and file paths intact.