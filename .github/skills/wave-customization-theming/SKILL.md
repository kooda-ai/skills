---
name: wave-customization-theming
description: 'Use when: working with Wave themes, theme installation, theme activation, theme structure, theme views, theme pages, theme assets, creating themes, logo/favicon/color customization, auth screen customization, and Wave theming/code layout questions. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave theme install, activate, create, customize, or theme-file structure task'
---

# Wave Customization And Theming

## Purpose
Use this skill for Wave theme selection, activation, creation, asset wiring, and basic customization surfaces such as logo, favicon, colors, and auth appearance.

## Source Rule
1. Before giving final theme steps, file paths, or customization guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave theming or customization topic.
2. Do not add theme structure, route mapping, view namespace behavior, asset commands, logo paths, favicon paths, or config keys unless they are confirmed in the current Wave docs.
3. If the task moves into broader Laravel, Vite, Folio, Volt, or DevDojo Auth behavior, say that the Wave docs defer to those products.
4. Keep examples close to documented file paths, helpers, and commands.

## Reference Map
- Theme installation, activation, structure, assets, and basic customization surfaces: [themes-and-customization.md](./references/themes-and-customization.md)

## Related Wave Skills
- Use `wave-installation-development` for first-run setup, defaults, stack details, and documented development starting points.
- Use `wave-plugins-concepts` for Volt pages, Folio route mapping, plugin structure, and Filament-with-Volt patterns.
- Use `wave-auth-users` for auth setup pages, profile routes, custom profile fields, and user-facing auth flows.

## Workflow
1. Identify the surface: theme install, theme activation, theme structure, theme creation, theme assets, logo/favicon/color customization, or auth appearance.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use documented theme folders, asset paths, and admin activation steps only.
5. For auth appearance changes, keep the answer inside the documented `/auth/setup` boundary unless the user asks for deeper Auth docs.
6. Omit unconfirmed theming behavior.

## Confirmed Core Patterns
- Themes are installed in `resources/themes/{theme}` and activated from `/admin/themes`.
- The docs say downloaded theme folders should be renamed to the theme name before placement in `resources/themes`.
- After activating a theme, the docs say `npm run dev` may need to be stopped and restarted.
- Active theme views live in `resources/themes/{theme}` and can be resolved with the `theme::` namespace, for example `return view('theme::home');`.
- Theme pages live in `resources/themes/{theme}/pages` and are mapped to routes.
- Documented theme assets live at `resources/themes/{theme}/assets/css/app.css` and `resources/themes/{theme}/assets/js/app.js`.
- The docs say `npm run dev` handles asset compilation and HMR, and `npm run build` builds production assets.
- The active theme is tracked in root `theme.json`, and the docs show `vite.config.js` reading that file to choose active theme assets.
- A minimal custom theme in the docs uses a lowercase folder, `theme.json`, and `theme.jpg`.
- The documented theme structure includes `assets`, `components`, `pages`, and `partials`.
- Theme layouts include authenticated and guest layouts: `app.blade.php` and `marketing.blade.php`.
- The docs show `@filamentStyles` and `@livewireStyles` before `@vite(...)` in theme layouts.
- Logos are customized in `resources/views/components/logo.blade.php` and `resources/views/components/logo-icon.blade.php`.
- The docs say logo markup should preserve `{{ $attributes->merge([...]) }}` for class forwarding.
- Favicons are documented at `public/wave/favicon.png`, `public/wave/favicon-dark.png`, and optionally `/public/favicon.ico`.
- The default Wave color is documented as `primary_color` in `config/wave.php`.
- Authentication view customization is documented through `/auth/setup`.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact theme or customization topic.
- Every folder path, asset path, route, config key, helper, and command is traceable to the current Wave docs.
- Deeper Laravel, Vite, Folio, Volt, or DevDojo Auth details are not inferred beyond what the Wave docs confirm.
