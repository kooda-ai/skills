---
name: filament-5-advanced-assets
description: 'Use when: working with Filament 5 Advanced Registering assets, FilamentAsset::register(), Css::make(), Js::make(), AlpineComponent::make(), php artisan filament:assets, plugin package asset registration, lazy-loaded CSS/JS with loadedOnRequest(), x-load-css, x-load-js, getStyleHref(), getScriptSrc(), getAlpineComponentSrc(), registerScriptData(), registerCssVariables(), URL assets, Vite::asset(), esbuild, and Tailwind CSS in plugins. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Asset registration task, CSS/JS/Alpine asset, plugin package assets, lazy loading, Vite/esbuild, script data, CSS variables, or code to review'
---

# Filament 5 Advanced Registering Assets

## Purpose
Use this skill to create, review, or explain Filament 5 asset registration using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Advanced Registering assets topic.
2. Do not add asset classes, methods, lifecycle behavior, load timing, package behavior, build-tool behavior, commands, paths, namespaces, or examples unless they appear in the retrieved documentation or the loaded reference files.
3. If the current Context7 lookup conflicts with a reference file, the current Context7 lookup wins.
4. If a requested asset topic is not confirmed, run a narrower Context7 lookup or say that the current documentation context did not confirm it.
5. Keep examples close to documented snippets and preserve documented method names, class names, argument names, command names, paths, and Blade attributes.

## Reference Map
- Asset manager, `FilamentAsset` facade, plugin package registration, asset IDs, and publishing: [asset-manager.md](./references/asset-manager.md)
- CSS files, Tailwind CSS in plugins, lazy CSS, URL CSS assets, and CSS variables: [css-assets.md](./references/css-assets.md)
- JavaScript files, lazy JavaScript, script data, URL JavaScript assets, Vite-compiled JavaScript, and asynchronous Alpine components: [javascript-assets.md](./references/javascript-assets.md)

## Workflow
1. Identify the asset surface: global registration, plugin registration, CSS file, Tailwind CSS in plugins, lazy CSS, CSS URL asset, CSS variables, JavaScript file, lazy JavaScript, script data, JavaScript URL asset, Vite-compiled JavaScript, asynchronous Alpine component, or asset publishing.
2. Run a narrow Context7 query for the exact asset topic before producing code.
3. Load the relevant reference file from the map above.
4. For asset registration placement, use `FilamentAsset` in the `boot()` method of a service provider only as documented. The docs confirm application service providers such as `AppServiceProvider` and plugin service providers.
5. For plugin assets, pass the Composer package name with the documented `package:` argument to `FilamentAsset::register()` and to asset URL helpers when lazy loading plugin assets.
6. For CSS assets, use only documented `Css::make()`, `loadedOnRequest()`, `FilamentAsset::getStyleHref()`, `x-load-css`, URL CSS assets, and `FilamentAsset::registerCssVariables()` patterns confirmed by the lookup.
7. For Tailwind CSS in plugins, include the documented warning that Tailwind builds are unique to each application, the documented `@source` vendor-directory pattern, and the documented default-stylesheet caveat only when the lookup confirms them.
8. For JavaScript assets, use only documented `Js::make()`, `loadedOnRequest()`, `FilamentAsset::getScriptSrc()`, `x-load-js`, `FilamentAsset::registerScriptData()`, URL JavaScript assets, and Vite registration patterns confirmed by the lookup.
9. For JavaScript that uses imports or npm dependencies, include the documented constraint that `php artisan filament:assets` copies files as-is, and use the documented Vite workflow or asynchronous Alpine esbuild workflow only when confirmed.
10. For asynchronous Alpine components, use only documented `AlpineComponent::make()`, `FilamentAsset::getAlpineComponentSrc()`, `x-load`, `x-load-src`, `x-data`, esbuild installation, build commands, and component file patterns confirmed by the lookup.
11. Finish by checking that every method, class, facade, argument, Blade attribute, command, path, load-timing claim, build-tool claim, and code example is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Filament packages share an asset management system for registering CSS and JavaScript files consumed by Blade views.
- `Filament\Support\Facades\FilamentAsset` registers files into the asset system.
- Registered filesystem assets are copied into `/public` when `php artisan filament:assets` runs.
- Asset IDs are chosen by the developer, used as copied file names, and used to reference assets in Blade views.
- `FilamentAsset::register()` accepts an array of assets and is used in the `boot()` method of a service provider.
- Plugin assets pass the Composer package name with `package: 'danharrin/filament-blog'`, and plugin assets are copied into their own directory inside `/public`.
- CSS assets use `Filament\Support\Assets\Css`; JavaScript assets use `Filament\Support\Assets\Js`; asynchronous Alpine components use `Filament\Support\Assets\AlpineComponent`.
- Registered CSS files load in the `<head>` of every Filament page by default; registered JavaScript files load at the bottom of every Filament page by default.
- `loadedOnRequest()` prevents automatic loading so assets can be loaded on demand with the documented Alpine lazy-load directives.
- URL-based CSS and JavaScript assets are loaded on every page as normal but are not copied into `/public` by `php artisan filament:assets`.
- `FilamentAsset::registerScriptData()` makes backend data available to JavaScript through `window.filamentData`.
- `FilamentAsset::registerCssVariables()` makes backend data available to CSS through CSS variables.
- For JavaScript that needs bundling, the docs use Vite for compiled JavaScript files and esbuild for asynchronous Alpine components.

## Completion Check
- The answer uses only APIs, commands, paths, examples, lifecycle details, and load behavior confirmed by the current Context7 lookup and the loaded reference files.
- Each asset ID, package argument, helper method, Blade directive, build command, import, namespace, and code example is traceable to Filament 5.x documentation.
- Unconfirmed asset APIs are not inferred from Filament 4.x, older examples, Laravel habits, Vite habits, Alpine habits, package source code, or memory.
- If the user asks for panel-specific assets, render hooks, styling hooks, custom fields, or plugin architecture beyond the asset-registration docs, run a fresh Context7 lookup and load the matching Filament 5 skill before writing code.
- Code examples keep documented namespaces, method names, argument names, command strings, paths, Blade attributes, and helper names intact.