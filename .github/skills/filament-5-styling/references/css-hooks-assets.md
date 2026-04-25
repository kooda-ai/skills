# CSS Hooks and Assets

Use this reference after a fresh Context7 lookup for the exact Filament 5 styling, CSS hook, or asset topic.

## CSS Hook Classes
- Filament uses CSS hook classes to allow various HTML elements to be customized using CSS.
- The docs recommend using browser developer tools to inspect the elements to customize and then targeting their hook classes.
- All hook classes are prefixed with `fi-`.
- Hook classes are usually near the start of the class list, but may appear further down if applied conditionally with JavaScript or Blade.
- If the needed hook class is missing, the docs say not to hack around it because that may expose styling customizations to breaking changes in future releases. They recommend opening a pull request to add the hook class.

## Applying Styles to Hooks
- The docs use `.fi-sidebar` as an example hook class for customizing the sidebar color:

```css
.fi-sidebar {
    background-color: #fafafa;
}
```

- Since Filament is built on Tailwind CSS, the docs show Tailwind's `@apply` directive:

```css
.fi-sidebar {
    @apply bg-gray-50 dark:bg-gray-950;
}
```

- The docs state that `!important` may occasionally be needed to override existing styles, but should be used sparingly:

```css
.fi-sidebar {
    @apply bg-gray-50 dark:bg-gray-950 !important;
}
```

- The docs also show applying `!important` to specific Tailwind classes by prefixing the class with `!`:

```css
.fi-sidebar {
    @apply !bg-gray-50 dark:!bg-gray-950;
}
```

## Hook Class Abbreviations
- `fi` is short for Filament.
- `fi-ac` is used for classes in the Actions package.
- `fi-fo` is used for classes in the Forms package.
- `fi-in` is used for classes in the Infolists package.
- `fi-no` is used for classes in the Notifications package.
- `fi-sc` is used for classes in the Schema package.
- `fi-ta` is used for classes in the Tables package.
- `fi-wi` is used for classes in the Widgets package.
- `btn` is short for button.
- `col` is short for column.
- `ctn` is short for container.
- `wrp` is short for wrapper.

## Publishing Blade Views
- The docs say developers may be tempted to publish internal Blade views for customization, but Filament does not recommend this because it introduces breaking changes in future updates.
- The docs recommend CSS hook classes wherever possible.
- If internal Blade views are published, the docs say to lock all Filament packages to a specific version in `composer.json`, update manually by bumping the version, and test the entire application after each update.

## Panel-Specific Assets
- Register assets that should only load on pages within a specific panel with `assets()` in panel configuration.

```php
use Filament\Panel;
use Filament\Support\Assets\Css;
use Filament\Support\Assets\Js;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->assets([
            Css::make('custom-stylesheet', resource_path('css/custom.css')),
            Js::make('custom-script', resource_path('js/custom.js')),
        ]);
}
```

- Before those assets can be used, run:

```bash
php artisan filament:assets
```

## Global CSS Asset Registration
- Filament packages share an asset management system for CSS and JavaScript files consumed by Blade views.
- The `Filament\Support\Facades\FilamentAsset` facade registers files into the asset system.
- Registered files may come from anywhere in the filesystem, then are copied into `/public` when `php artisan filament:assets` is run.
- Assets have a unique ID, which is used as the copied file name and to reference the asset in Blade views.
- `FilamentAsset` should be used in the `boot()` method of a service provider.
- Register a CSS file with `FilamentAsset::register()` and `Filament\Support\Assets\Css`:

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('custom-stylesheet', __DIR__ . '/../../resources/css/custom.css'),
]);
```

- When `php artisan filament:assets` is run, the CSS file is copied into `/public` and loaded into all Blade views that use Filament.

## Plugin CSS Assets
- When registering assets for a plugin, pass the Composer package name as the second argument of `register()`:

```php
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    // ...
], package: 'danharrin/filament-blog');
```

- Plugin assets are copied into their own directory inside `/public` to avoid clashing with other plugins' files with the same names.
- The docs advise plugin developers not to build Tailwind CSS files into plugins in most cases.
- Instead, provide raw CSS files and instruct users to build the Tailwind CSS file themselves by adding the plugin vendor directory to their custom theme CSS file with `@source`:

```css
@import "tailwindcss";

@source '../../../../app/Filament/**/*';
@source '../../../../resources/views/filament/**/*';
@source '../../../../vendor/danharrin/filament-blog/resources/views/**/*'; /* Your plugin's vendor directory */
```

- The docs describe one situation where compiling and registering a Tailwind CSS-compiled stylesheet in a plugin may be recommended: a Panel Builder user uses the default stylesheet, does not compile CSS themselves, and the plugin uses utility classes not included in the default stylesheet.

## Lazy-Loaded CSS
- By default, registered CSS files load in the `<head>` of every Filament page.
- For CSS that is not required on every page, the docs show Alpine.js Lazy Load Assets with `x-load-css`.

```blade
<div
    x-data="{}"
    x-load-css="[@js(\Filament\Support\Facades\FilamentAsset::getStyleHref('custom-stylesheet'))]"
>
    <!-- ... -->
</div>
```

- Prevent a CSS file from loading automatically with `loadedOnRequest()`:

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('custom-stylesheet', __DIR__ . '/../../resources/css/custom.css')->loadedOnRequest(),
]);
```

- If the CSS file was registered to a plugin, pass the package as the second argument to `FilamentAsset::getStyleHref()`:

```blade
<div
    x-data="{}"
    x-load-css="[@js(\Filament\Support\Facades\FilamentAsset::getStyleHref('custom-stylesheet', package: 'danharrin/filament-blog'))]"
>
    <!-- ... -->
</div>
```

## CSS Assets From URLs
- CSS files can be registered from a URL.
- URL assets load on every page as normal, but are not copied into `/public` when `php artisan filament:assets` is run.

```php
use Filament\Support\Assets\Css;
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    Css::make('example-external-stylesheet', 'https://example.com/external.css'),
    Css::make('example-local-stylesheet', asset('css/local.css')),
]);
```

## CSS Variables
- For dynamic backend data in CSS files, register CSS variables with `FilamentAsset::registerCssVariables()` in the `boot()` method of a service provider:

```php
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::registerCssVariables([
    'background-image' => asset('images/background.jpg'),
]);
```

- Access registered variables from any CSS file:

```css
background-image: var(--background-image);
```