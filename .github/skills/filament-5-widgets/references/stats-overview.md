# Stats Overview Widgets

Use this reference only after a fresh Context7 lookup confirms the current stats overview widget topic.

## Creating a Stats Overview Widget
- Stats overview widgets display different stats in a single widget without a custom view.
- Generate one with:

```bash
php artisan make:filament-widget StatsOverview --stats-overview
```

- The command creates `StatsOverview.php`.
- Return `Stat` instances from `getStats()`:

```php
<?php

namespace App\Filament\Widgets;

use Filament\Widgets\StatsOverviewWidget as BaseWidget;
use Filament\Widgets\StatsOverviewWidget\Stat;

class StatsOverview extends BaseWidget
{
    protected function getStats(): array
    {
        return [
            Stat::make('Unique views', '192.1k'),
            Stat::make('Bounce rate', '21%'),
            Stat::make('Average time on page', '3:12'),
        ];
    }
}
```

## Descriptions and Icons
- `description()` adds additional information to a stat.
- `descriptionIcon()` adds an icon:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up'),
        Stat::make('Bounce rate', '21%')
            ->description('7% decrease')
            ->descriptionIcon('heroicon-m-arrow-trending-down'),
        Stat::make('Average time on page', '3:12')
            ->description('3% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up'),
    ];
}
```

- `descriptionIcon()` accepts a second parameter to place the icon before the description:

```php
use Filament\Support\Enums\IconPosition;
use Filament\Widgets\StatsOverviewWidget\Stat;

Stat::make('Unique views', '192.1k')
    ->description('32k increase')
    ->descriptionIcon('heroicon-m-arrow-trending-up', IconPosition::Before)
```

## Color
- A stat can use `color()`:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->color('success'),
        Stat::make('Bounce rate', '21%')
            ->description('7% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-down')
            ->color('danger'),
        Stat::make('Average time on page', '3:12')
            ->description('3% increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->color('success'),
    ];
}
```

## Extra HTML Attributes
- `extraAttributes()` passes extra HTML attributes to stats:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Processed', '192.1k')
            ->color('success')
            ->extraAttributes([
                'class' => 'cursor-pointer',
                'wire:click' => "\$dispatch('setStatusFilter', { filter: 'processed' })",
            ]),
        // ...
    ];
}
```

- The docs deliberately escape the `$` in `$dispatch()` because it must be passed directly to HTML, not treated as a PHP variable.

## Stat Charts
- `chart()` can be added or chained to a stat to provide historical data.
- `chart()` accepts an array of data points to plot:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

protected function getStats(): array
{
    return [
        Stat::make('Unique views', '192.1k')
            ->description('32k increase')
            ->descriptionIcon('heroicon-m-arrow-trending-up')
            ->chart([7, 2, 10, 3, 15, 4, 17])
            ->color('success'),
        // ...
    ];
}
```

## Polling
- By default, stats overview widgets refresh their data every 5 seconds.
- Customize polling with `$pollingInterval`:

```php
protected ?string $pollingInterval = '10s';
```

- Disable polling with:

```php
protected ?string $pollingInterval = null;
```

## Lazy Loading
- By default, widgets are lazy-loaded and only load when visible on the page.
- Disable lazy loading with:

```php
protected static bool $isLazy = false;
```

## Heading and Description
- Add heading and description text above the widget with `$heading` and `$description`:

```php
protected ?string $heading = 'Analytics';

protected ?string $description = 'An overview of some analytics.';
```

- Generate heading or description dynamically with `getHeading()` and `getDescription()`:

```php
protected function getHeading(): ?string
{
    return 'Analytics';
}

protected function getDescription(): ?string
{
    return 'An overview of some analytics.';
}
```
