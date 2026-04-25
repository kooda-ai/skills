# Asset Manager

Use this reference after a fresh Context7 lookup for the exact Filament 5 Advanced Registering assets topic.

## Introduction
- All packages in the Filament ecosystem share an asset management system.
- The asset system lets official plugins and third-party plugins register CSS and JavaScript files that can be consumed by Blade views.

## `FilamentAsset` Facade
- `Filament\Support\Facades\FilamentAsset` registers files into the asset system.
- Registered files may be sourced from anywhere in the filesystem.
- Filesystem assets are copied into the `/public` directory when the `php artisan filament:assets` command is run.
- Copying assets into `/public` lets Filament load them predictably in Blade views and lets third-party packages load assets without worrying about where they are located.
- Assets always have a unique ID chosen by the developer.
- The asset ID is used as the copied file name and as the reference for the asset in Blade views.
- If assets are registered for a plugin, IDs do not need to be protected from other plugins because the asset is copied into a directory named after the plugin.
- `FilamentAsset` should be used in the `boot()` method of a service provider.
- The docs confirm use inside an application service provider such as `AppServiceProvider`, or inside a plugin service provider.
- `FilamentAsset` has one main method, `register()`, which accepts an array of assets to register.

```php
use Filament\Support\Facades\FilamentAsset;

public function boot(): void
{
    // ...

    FilamentAsset::register([
        // ...
    ]);

    // ...
}
```

## Registering Assets for a Plugin
- When registering assets for a plugin, pass the Composer package name as the second argument of `register()`.
- Plugin assets are copied into their own directory inside `/public` to avoid clashes with other plugins' files with the same names.

```php
use Filament\Support\Facades\FilamentAsset;

FilamentAsset::register([
    // ...
], package: 'danharrin/filament-blog');
```

## Publishing
- Run the documented asset command after registering filesystem assets that need to be copied into `/public`:

```bash
php artisan filament:assets
```

## Decision Points
- Use `package:` when the asset belongs to a plugin.
- Use the documented CSS or JavaScript reference when choosing an asset class, load behavior, lazy-load helper, URL asset, data registration method, or build workflow.
- Do not introduce a generic asset class, publish command, package path, or service-provider lifecycle detail unless the current Context7 lookup confirms it.