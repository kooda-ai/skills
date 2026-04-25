# Widgets Overview and Dashboard

Use this reference only after a fresh Context7 lookup confirms the current Widgets topic.

## Widget Types and Creation
- Filament dashboards are made of widgets that display data in a specific way.
- Documented widget categories are stats, chart, table, and custom widgets.
- Create a widget with `php artisan make:filament-widget MyWidget`.
- The command asks which type of widget to create: Custom, Chart, Stats overview, or Table.

## Panel Registration and Default Widgets
- A widget can be registered in panel configuration with `widgets([...])`.
- The docs show `widgets([ClockWidgetWidget::class])` inside `public function panel(Panel $panel): Panel`.
- Default dashboard widgets can be disabled by setting the panel configuration widgets array to empty:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->widgets([]);
}
```

## Sorting Widgets
- Each widget class contains a `$sort` property that may change its order on the page relative to other widgets:

```php
protected static ?int $sort = 2;
```

## Customizing the Dashboard Page
- To customize the dashboard class, create `app/Filament/Pages/Dashboard.php` and extend `Filament\Pages\Dashboard`:

```php
<?php

namespace App\Filament\Pages;

use Filament\Pages\Dashboard as BaseDashboard;

class Dashboard extends BaseDashboard
{
    // ...
}
```

- Remove the original `Dashboard` class from panel configuration by discovering pages and setting `pages([])`:

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->discoverPages(in: app_path('Filament/Pages'), for: 'App\\Filament\\Pages')
        ->pages([]);
}
```

- If pages are not discovered in that directory, manually register the dashboard class in `pages()`:

```php
use App\Filament\Pages\Dashboard;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->pages([
            Dashboard::class,
        ]);
}
```

## Multiple Dashboards
- Multiple dashboards can be created by repeating the custom dashboard page process.
- New pages that extend `Dashboard` allow as many dashboards as needed.
- Extra dashboards need a URL path, otherwise they are at `/`:

```php
protected static string $routePath = 'finance';
```

- The dashboard title can be customized with `$title`:

```php
protected static ?string $title = 'Finance dashboard';
```

- The primary dashboard shown to a user is the first one they have access to, controlled by `canAccess()`, according to the defined navigation sort order.
- The default dashboard sort order is `-2`.
- Custom dashboard sort order can be controlled with `$navigationSort`:

```php
protected static ?int $navigationSort = 15;
```

## Dashboard Grid Columns
- A custom dashboard page can override `getColumns()` to define the widget grid:

```php
public function getColumns(): int | array
{
    return 2;
}
```

- Responsive columns can be returned as an array keyed by breakpoint:

```php
public function getColumns(): int | array
{
    return [
        'md' => 4,
        'xl' => 5,
    ];
}
```

## Widget Width
- A widget can customize its width with the `$columnSpan` property.
- The docs state the value may be a number between 1 and 12, or `full` for full page width:

```php
protected int | string | array $columnSpan = 'full';
```

- Responsive widget widths can use an array keyed by breakpoint:

```php
protected int | string | array $columnSpan = [
    'md' => 2,
    'xl' => 3,
];
```

## Conditionally Hiding Widgets
- Override static `canView()` on widgets to conditionally hide them:

```php
public static function canView(): bool
{
    return auth()->user()->isAdmin();
}
```

## Table Widgets
- Table widgets are generated with:

```bash
php artisan make:filament-widget LatestOrders --table
```

- The docs state the generated widget file can be edited to customize the table.
- For table internals, load the Filament 5 Tables skill after confirming the table topic in Context7.

## Custom Widgets
- Custom widgets can be generated with:

```bash
php artisan make:filament-widget BlogPostsOverview
```

- The command creates two files: a widget class in the `/Widgets` directory of the Filament directory, and a view in the `/widgets` directory of the Filament views directory.
- The class is a Livewire component, so Livewire features are available.
- The Blade view can contain any HTML.
- Public Livewire properties are accessible in the view.
- The Livewire component instance is accessible in the view using `$this`.

## Filtering Widget Data With a Form
- A dashboard can add a form that filters data displayed across all widgets.
- When filters update, widgets reload with the new data.
- First replace the original Dashboard page.
- Add `HasFiltersForm` and implement `filtersForm(Schema $schema): Schema`:

```php
use Filament\Forms\Components\DatePicker;
use Filament\Pages\Dashboard as BaseDashboard;
use Filament\Pages\Dashboard\Concerns\HasFiltersForm;
use Filament\Schemas\Components\Section;
use Filament\Schemas\Schema;

class Dashboard extends BaseDashboard
{
    use HasFiltersForm;

    public function filtersForm(Schema $schema): Schema
    {
        return $schema
            ->components([
                Section::make()
                    ->schema([
                        DatePicker::make('startDate'),
                        DatePicker::make('endDate'),
                        // ...
                    ])
                    ->columns(3),
            ]);
    }
}
```

- Widgets that require filter data add `InteractsWithPageFilters` and access `$this->pageFilters`:

```php
use Filament\Widgets\Concerns\InteractsWithPageFilters;

class BlogPostsOverview extends StatsOverviewWidget
{
    use InteractsWithPageFilters;

    public function getStats(): array
    {
        $startDate = $this->pageFilters['startDate'] ?? null;
        $endDate = $this->pageFilters['endDate'] ?? null;

        // ...
    }
}
```

- The docs state `$this->pageFilters` always reflects current form data.
- The docs state this data is raw and not intended for anything other than querying the database; ensure the data is valid before using it.

## Filtering Widget Data With an Action Modal
- The filters form can be swapped for an action modal opened from a page header button.
- Use `HasFiltersAction` instead of `HasFiltersForm`.
- Register `FilterAction` in `getHeaderActions()`:

```php
use Filament\Forms\Components\DatePicker;
use Filament\Pages\Dashboard as BaseDashboard;
use Filament\Pages\Dashboard\Actions\FilterAction;
use Filament\Pages\Dashboard\Concerns\HasFiltersAction;

class Dashboard extends BaseDashboard
{
    use HasFiltersAction;

    protected function getHeaderActions(): array
    {
        return [
            FilterAction::make()
                ->schema([
                    DatePicker::make('startDate'),
                    DatePicker::make('endDate'),
                    // ...
                ]),
        ];
    }
}
```

- Handling data from the filter action is the same as handling data from the filters header form, except the data is validated before being passed to the widget.
- `InteractsWithPageFilters` still applies.

## Persisting Widget Filters
- By default, dashboard filters persist in the user's session between page loads.
- Disable session persistence with `$persistsFiltersInSession`:

```php
use Filament\Pages\Dashboard as BaseDashboard;
use Filament\Pages\Dashboard\Concerns\HasFiltersForm;

class Dashboard extends BaseDashboard
{
    use HasFiltersForm;

    protected bool $persistsFiltersInSession = false;
}
```

- Alternatively, override `persistsFiltersInSession()`:

```php
use Filament\Pages\Dashboard as BaseDashboard;
use Filament\Pages\Dashboard\Concerns\HasFiltersForm;

class Dashboard extends BaseDashboard
{
    use HasFiltersForm;

    public function persistsFiltersInSession(): bool
    {
        return false;
    }
}
```
