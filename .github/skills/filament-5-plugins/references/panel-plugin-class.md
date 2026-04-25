# Panel Plugin Class

Use this reference after a fresh Context7 lookup for the exact Filament 5 Panel Plugin topic.

## Package Foundation
- The docs state the basis of Filament plugins is Laravel packages.
- Filament plugins are installed into Filament projects through Composer.
- Plugin packages follow standard Laravel package techniques, such as using service providers to register routes, views, and translations.
- Filament plugins allow reusable features to be shipped and consumed for any Filament panel.
- Plugins can be added to each panel one at a time and configured differently per panel.

## Required Class Shape
- A panel plugin class implements `Filament\Contracts\Plugin`.
- The class interacts with a panel configuration file.
- Three methods are required: `getId()`, `register(Panel $panel)`, and `boot(Panel $panel)`.
- `getId()` returns the unique identifier of the plugin among other plugins.
- The docs warn that the ID should be specific enough not to clash with other plugins in the same project.
- `register()` can use any configuration option available to the panel, including resources, custom pages, themes, render hooks, and more.
- `boot()` runs only when the panel that the plugin is registered to is actually in use.
- The docs state `boot()` is executed by a middleware class.

```php
<?php

namespace DanHarrin\FilamentBlog;

use DanHarrin\FilamentBlog\Pages\Settings;
use DanHarrin\FilamentBlog\Resources\CategoryResource;
use DanHarrin\FilamentBlog\Resources\PostResource;
use Filament\Contracts\Plugin;
use Filament\Panel;

class BlogPlugin implements Plugin
{
    public function getId(): string
    {
        return 'blog';
    }

    public function register(Panel $panel): void
    {
        $panel
            ->resources([
                PostResource::class,
                CategoryResource::class,
            ])
            ->pages([
                Settings::class,
            ]);
    }

    public function boot(Panel $panel): void
    {
        //
    }
}
```

## Adding a Plugin to a Panel
- Users add a plugin to a panel by instantiating the plugin class and passing it to `plugin()` in the panel configuration.

```php
use DanHarrin\FilamentBlog\BlogPlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->plugin(new BlogPlugin());
}
```

## Fluent Instantiation
- The docs suggest adding `make()` to provide a fluent interface for instantiating the plugin.
- The docs state that using the container through `app()` allows the plugin object to be replaced with a different implementation at runtime.

```php
use Filament\Contracts\Plugin;

class BlogPlugin implements Plugin
{
    public static function make(): static
    {
        return app(static::class);
    }

    // ...
}
```

```php
use DanHarrin\FilamentBlog\BlogPlugin;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->plugin(BlogPlugin::make());
}
```

## Per-Panel Configuration
- The docs suggest adding both a setter and getter for each plugin option.
- The setter stores the user preference in a property on the plugin object.
- The setter returns `static` to allow fluent chaining.
- The getter retrieves the stored preference.
- The docs state `register()` is executed after the user configures the plugin, so preferences can be accessed inside `register()`.

```php
use DanHarrin\FilamentBlog\Resources\AuthorResource;
use Filament\Contracts\Plugin;
use Filament\Panel;

class BlogPlugin implements Plugin
{
    protected bool $hasAuthorResource = false;

    public function authorResource(bool $condition = true): static
    {
        $this->hasAuthorResource = $condition;

        return $this;
    }

    public function hasAuthorResource(): bool
    {
        return $this->hasAuthorResource;
    }

    public function register(Panel $panel): void
    {
        if ($this->hasAuthorResource()) {
            $panel->resources([
                AuthorResource::class,
            ]);
        }
    }

    // ...
}
```

- Plugin configuration can be accessed from outside the plugin class by passing the unique ID to `filament()`.

```php
filament('blog')->hasAuthorResource()
```

- The docs show an optional static `get()` helper for type safety and IDE autocompletion.

```php
use Filament\Contracts\Plugin;

class BlogPlugin implements Plugin
{
    public static function get(): static
    {
        return filament(app(static::class)->getId());
    }

    // ...
}
```

```php
BlogPlugin::get()->hasAuthorResource()
```