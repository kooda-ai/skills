# Distributed Panels

Use this reference after a fresh Context7 lookup for the exact Filament 5 panel plugin or distributed panel topic.

## Documented Pattern
- The docs state a Laravel package can distribute an entire panel.
- The docs state the panel configuration class extends `Filament\PanelProvider`.
- The docs state `PanelProvider` is a standard Laravel service provider.
- The docs show registering the panel provider in Composer metadata under `extra.laravel.providers`.

## Panel Provider Example

```php
<?php

namespace DanHarrin\FilamentBlog;

use Filament\Panel;
use Filament\PanelProvider;

class BlogPanelProvider extends PanelProvider
{
    public function panel(Panel $panel): Panel
    {
        return $panel
            ->id('blog')
            ->path('blog')
            ->resources([
                // ...
            ])
            ->pages([
                // ...
            ])
            ->widgets([
                // ...
            ])
            ->middleware([
                // ...
            ])
            ->authMiddleware([
                // ...
            ]);
    }
}
```

## Composer Provider Registration

```json
"extra": {
    "laravel": {
        "providers": [
            "DanHarrin\\FilamentBlog\\BlogPanelProvider"
        ]
    }
}
```

## Use Boundaries
- Use the distributed panel pattern only when the task is about shipping a complete panel from a package.
- For module plugins that add resources, pages, and widgets to an existing panel, use [module-panel-registration.md](./module-panel-registration.md) instead.
- Do not add middleware details beyond the documented `middleware()` and `authMiddleware()` placeholders unless a fresh Context7 lookup confirms them.