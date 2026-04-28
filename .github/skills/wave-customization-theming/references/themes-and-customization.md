# Themes And Customization

## Theme Installation And Activation
- Themes are installed under `resources/themes/{theme}`.
- Downloaded theme folders should be renamed to the real theme name before placement in `resources/themes`.
- Themes are activated from `/admin/themes`.
- After activation, the docs say `npm run dev` may need to be restarted.

## Theme Structure
- Active theme views live in `resources/themes/{theme}`.
- The active theme is available through the `theme::` namespace, for example `return view('theme::home');`.
- The documented theme structure includes `assets`, `components`, `pages`, and `partials`.
- Theme layouts include `app.blade.php` for authenticated users and `marketing.blade.php` for guests.

## Theme Pages And Assets
- Theme pages live in `resources/themes/{theme}/pages` and are route-mapped.
- Theme assets live at `resources/themes/{theme}/assets/css/app.css` and `resources/themes/{theme}/assets/js/app.js`.
- The docs show `@filamentStyles` and `@livewireStyles` before `@vite(...)` in theme layouts.
- `npm run dev` is documented for HMR and `npm run build` for production assets.
- Root `theme.json` is used by `vite.config.js` to select the active theme assets.

## Basic Customization Surfaces
- Logos live in `resources/views/components/logo.blade.php` and `resources/views/components/logo-icon.blade.php`.
- Logo markup should preserve `{{ $attributes->merge([...]) }}`.
- Favicons are documented at `public/wave/favicon.png`, `public/wave/favicon-dark.png`, and optionally `/public/favicon.ico`.
- The default color is documented as `primary_color` in `config/wave.php`.
- Auth appearance customization is documented through `/auth/setup`.
