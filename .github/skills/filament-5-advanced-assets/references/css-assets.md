# CSS Assets

Use this reference after a fresh Context7 lookup for the exact Filament 5 CSS asset topic.

## Registering CSS Files
- Register a CSS file with `FilamentAsset::register()` in the `boot()` method of a service provider.
- Pass an array of `Filament\Support\Assets\Css` objects.
- Each `Css` object has a unique ID and a path to the CSS file.
- The docs use `__DIR__` to generate a relative path from the current file.
- If the code is added to `/app/Providers/AppServiceProvider.php`, the documented example path points to `/resources/css/custom.css`.
- When `php artisan filament:assets` runs, the CSS file is copied into `/public` and loaded into all Blade views that use Filament.

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('custom-stylesheet', __DIR__ . '/../../resources/css/custom.css'),
]);
```

## Tailwind CSS in Plugins
- Tailwind builds are unique to every application and contain only the utility classes actually used in that application.
- The docs say plugin developers probably should not build Tailwind CSS files into a plugin.
- Instead, provide raw CSS files and instruct users to build the Tailwind CSS file themselves.
- To include plugin utility classes, users add the plugin vendor directory to their custom theme CSS file with `@source`.

```css
@import "tailwindcss";

@source '../../../../app/Filament/**/*';
@source '../../../../resources/views/filament/**/*';
@source '../../../../vendor/danharrin/filament-blog/resources/views/**/*'; /* Your plugin's vendor directory */
```

- If Panel Builder users have a custom theme, they are already building their own CSS file with Tailwind CSS.
- If Panel Builder users use the default stylesheet, utility classes used by a plugin may not be included in the final CSS file.
- The docs describe that as one of the few situations where compiling and registering a Tailwind CSS-compiled stylesheet in a plugin may be recommended.

## Lazy Loading CSS
- By default, CSS files registered with the asset system are loaded in the `<head>` of every Filament page.
- For CSS that is heavy or not required on every page, use the Alpine.js Lazy Load Assets package bundled with Filament.
- The `x-load-css` directive loads CSS files into the page `<head>` when the element is loaded onto the page.

```blade
<div
    x-data="{}"
    x-load-css="[@js(\Filament\Support\Facades\FilamentAsset::getStyleHref('custom-stylesheet'))]"
>
    <!-- ... -->
</div>
```

- Prevent automatic CSS loading with `loadedOnRequest()`:

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('custom-stylesheet', __DIR__ . '/../../resources/css/custom.css')->loadedOnRequest(),
]);
```

- If the CSS file was registered to a plugin, pass the plugin package name to `FilamentAsset::getStyleHref()`:

```blade
<div
    x-data="{}"
    x-load-css="[@js(\Filament\Support\Facades\FilamentAsset::getStyleHref('custom-stylesheet', package: 'danharrin/filament-blog'))]"
>
    <!-- ... -->
</div>
```

## CSS Files from a URL
- CSS files may be registered from a URL.
- URL assets are loaded on every page as normal.
- URL assets are not copied into `/public` when `php artisan filament:assets` runs.
- The docs describe this as useful for external stylesheets from a CDN or stylesheets already compiled directly into `/public`.

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('example-external-stylesheet', 'https://example.com/external.css'),
    Css::make('example-local-stylesheet', asset('css/local.css')),
]);
```

## CSS Variables
- For dynamic backend data in CSS files, use `FilamentAsset::registerCssVariables()` in the `boot()` method of a service provider.

```php
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::registerCssVariables([
    'background-image' => asset('images/background.jpg'),
]);
```

- Registered variables can be accessed from any CSS file:

```css
background-image: var(--background-image);
```

## Completion Check
- Confirm whether the CSS asset should load on every Filament page or only on request.
- Confirm whether the CSS asset belongs to a plugin and therefore needs a `package:` argument when registered or lazily referenced.
- Confirm whether the asset is a filesystem asset copied by `php artisan filament:assets` or a URL asset that is not copied.
- For plugin Tailwind CSS, include only the documented custom-theme `@source` guidance and default-stylesheet caveat.