# JavaScript and Alpine Assets

Use this reference after a fresh Context7 lookup for the exact Filament 5 JavaScript or Alpine asset topic.

## Registering JavaScript Files
- Register a JavaScript file with `FilamentAsset::register()` in the `boot()` method of a service provider.
- Pass an array of `Filament\Support\Assets\Js` objects.
- Each `Js` object has a unique ID and a path to the JavaScript file.
- The docs use `__DIR__` to generate a relative path from the current file.
- If the code is added to `/app/Providers/AppServiceProvider.php`, the documented example path points to `/resources/js/custom.js`.
- When `php artisan filament:assets` runs, the JavaScript file is copied into `/public` and loaded into all Blade views that use Filament.

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Js::make('custom-script', __DIR__ . '/../../resources/js/custom.js'),
]);
```

## Lazy Loading JavaScript
- By default, JavaScript files registered with the asset system are loaded at the bottom of every Filament page.
- For JavaScript that is heavy or not required on every page, use the Alpine.js Lazy Load Assets package bundled with Filament.
- The `x-load-js` directive loads JavaScript files at the bottom of the page when the element is loaded onto the page.

```blade
<div
    x-data="{}"
    x-load-js="[@js(\Filament\Support\Facades\FilamentAsset::getScriptSrc('custom-script'))]"
>
    <!-- ... -->
</div>
```

- Prevent automatic JavaScript loading with `loadedOnRequest()`:

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Js::make('custom-script', __DIR__ . '/../../resources/js/custom.js')->loadedOnRequest(),
]);
```

- If the JavaScript file was registered to a plugin, pass the plugin package name to `FilamentAsset::getScriptSrc()`:

```blade
<div
    x-data="{}"
    x-load-js="[@js(\Filament\Support\Facades\FilamentAsset::getScriptSrc('custom-script', package: 'danharrin/filament-blog'))]"
>
    <!-- ... -->
</div>
```

## Script Data
- For backend data that should be available to JavaScript files, use `FilamentAsset::registerScriptData()` in the `boot()` method of a service provider.

```php
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::registerScriptData([
    'user' => [
        'name' => auth()->user()?->name,
    ],
]);
```

- Registered script data is available at runtime through `window.filamentData`:

```js
window.filamentData.user.name // 'Dan Harrin'
```

## JavaScript Files from a URL
- JavaScript files may be registered from a URL.
- URL assets are loaded on every page as normal.
- URL assets are not copied into `/public` when `php artisan filament:assets` runs.
- The docs describe this as useful for external scripts from a CDN or scripts already compiled directly into `/public`.

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Js::make('example-external-script', 'https://example.com/external.js'),
    Js::make('example-local-script', asset('js/local.js')),
]);
```

## Vite-Compiled JavaScript Files
- The `php artisan filament:assets` command copies files as-is into `/public` without bundling or resolving dependencies.
- If a JavaScript file uses `import` statements to pull in npm packages, the browser will not be able to resolve them after a plain asset copy.
- JavaScript files that require bundling should be compiled with Vite first, then registered as URL-based assets.
- The docs add the custom JavaScript file as an entry point in `vite.config.js`:

```js
import { defineConfig } from 'vite'

import laravel from 'laravel-vite-plugin'

export default defineConfig({
    plugins: [
        laravel({
            input: [
                'resources/css/app.css',
                'resources/js/app.js',
                'resources/js/timezone.js', // Your custom script
            ],
        }),
    ],
})
```

- Compile the assets with Vite:

```bash
npm run build
```

- Register the compiled asset using `Vite::asset()` to resolve the versioned URL:

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;
use Illuminate\Support\Facades\Vite;

FilamentAsset::register([
    Js::make('timezone', Vite::asset('resources/js/timezone.js')),
]);
```

- The documented Vite approach also works for TypeScript files or any JavaScript that needs a build step.
- Since `Vite::asset()` returns a URL, the asset is not copied by `php artisan filament:assets`; it is served from Vite's build output.
- If JavaScript must be bundled for an asynchronous Alpine component, the docs say to consider using esbuild instead.

## Asynchronous Alpine.js Components
- For Alpine.js-based components that need external JavaScript libraries, the docs describe storing the compiled JavaScript and Alpine component in a separate file and loading it whenever the component is rendered.
- The docs install esbuild with NPM:

```bash
npm install esbuild --save-dev
```

- The documented build script example compiles `resources/js/components/test-component.js` into `resources/js/dist/components/test-component.js`.
- The documented component file exports a function:

```js
export default function testComponent({
    state,
}) {
    return {
        state,

        // You can define any other Alpine.js properties here.

        init() {
            // Initialise the Alpine component here, if you need to.
        },

        // You can define any other Alpine.js functions here.
    }
}
```

- Compile once with:

```bash
node bin/build.js
```

- Watch for changes with:

```bash
node bin/build.js --dev
```

- Register the compiled Alpine component with `Filament\Support\Assets\AlpineComponent` in the `boot()` method of a service provider:

```php
use Filament\Support\Assets\AlpineComponent;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    AlpineComponent::make('test-component', __DIR__ . '/../../resources/js/dist/components/test-component.js'),
]);
```

- When `php artisan filament:assets` runs, the compiled file is copied into `/public`.
- Load the asynchronous Alpine component in a view with `x-load` attributes and `FilamentAsset::getAlpineComponentSrc()`:

```blade
<div
    x-load
    x-load-src="{{ \Filament\Support\Facades\FilamentAsset::getAlpineComponentSrc('test-component') }}"
    x-data="testComponent({
        state: $wire.{{ $applyStateBindingModifiers("\$entangle('{$statePath}')") }},
    })"
>
    <input x-model="state" />
</div>
```

- The documented example is for a custom form field and passes `state` as a parameter to `testComponent()`.
- The docs say any parameters may be passed and accessed in `testComponent()`.
- If the code is not for a custom form field, the docs say the `state` parameter in the example can be ignored.
- The `x-load` attributes come from the Async Alpine package, and the docs say any features of that package can be used.

## Completion Check
- Confirm whether the JavaScript asset should load on every Filament page or only on request.
- Confirm whether the JavaScript asset belongs to a plugin and therefore needs a `package:` argument when registered or lazily referenced.
- Confirm whether the asset is a filesystem asset copied by `php artisan filament:assets` or a URL asset that is not copied.
- If the JavaScript uses imports or npm dependencies, use the documented Vite or esbuild workflow instead of registering the source file directly.