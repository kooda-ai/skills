# Chart Widgets

Use this reference only after a fresh Context7 lookup confirms the current chart widget topic.

## Creating a Chart Widget
- Filament includes chart widget templates for real-time, interactive charts.
- Generate a chart widget with:

```bash
php artisan make:filament-widget BlogPostsChart --chart
```

- A single `ChartWidget` class is used for all charts.
- The chart type is set by `getType()`.
- `$heading` sets the heading that describes the chart.
- For a dynamic heading, override `getHeading()`.
- `getData()` returns an array of datasets and labels.
- Each dataset is a labeled array of points to plot.
- Each label is a string.
- The returned structure is identical to the Chart.js library, which Filament uses to render charts.

```php
<?php

namespace App\Filament\Widgets;

use Filament\Widgets\ChartWidget;

class BlogPostsChart extends ChartWidget
{
    protected ?string $heading = 'Blog Posts';

    protected function getData(): array
    {
        return [
            'datasets' => [
                [
                    'label' => 'Blog posts created',
                    'data' => [0, 10, 5, 2, 21, 32, 45, 74, 65, 45, 77, 89],
                ],
            ],
            'labels' => ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        ];
    }

    protected function getType(): string
    {
        return 'line';
    }
}
```

## Available Chart Types
- The docs list these chart types: bar, bubble, doughnut, line, pie, polar area, radar, and scatter.
- A bar chart can be used by returning `'bar'` from `getType()`.

## Color
- The chart data color can be customized with `$color`:

```php
protected string $color = 'info';
```

- For further color customization or multiple dataset colors, use Chart.js color options in `getData()`:

```php
protected function getData(): array
{
    return [
        'datasets' => [
            [
                'label' => 'Blog posts created',
                'data' => [0, 10, 5, 2, 21, 32, 45, 74, 65, 45, 77, 89],
                'backgroundColor' => '#36A2EB',
                'borderColor' => '#9BD0F5',
            ],
        ],
        'labels' => ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    ];
}
```

## Generating Data From an Eloquent Model
- To generate chart data from an Eloquent model, the docs recommend installing `flowframe/laravel-trend`.
- The docs show `Trend::model()`, `between()`, `perMonth()`, and `count()` with `TrendValue`:

```php
use Flowframe\Trend\Trend;
use Flowframe\Trend\TrendValue;

protected function getData(): array
{
    $data = Trend::model(BlogPost::class)
        ->between(
            start: now()->startOfYear(),
            end: now()->endOfYear(),
        )
        ->perMonth()
        ->count();

    return [
        'datasets' => [
            [
                'label' => 'Blog posts',
                'data' => $data->map(fn (TrendValue $value) => $value->aggregate),
            ],
        ],
        'labels' => $data->map(fn (TrendValue $value) => $value->date),
    ];
}
```

## Basic Select Filters
- Chart filters can change the data presented, commonly for a time period.
- Set the default filter value with `$filter`:

```php
public ?string $filter = 'today';
```

- Define `getFilters()` to return values and labels:

```php
protected function getFilters(): ?array
{
    return [
        'today' => 'Today',
        'week' => 'Last week',
        'month' => 'Last month',
        'year' => 'This year',
    ];
}
```

- Use the active filter value inside `getData()`:

```php
protected function getData(): array
{
    $activeFilter = $this->filter;

    // ...
}
```

## Custom Filters
- Schema components can be used to build custom filters for a chart widget.
- Use `HasFiltersSchema` and implement `filtersSchema()`:

```php
use Filament\Forms\Components\DatePicker;
use Filament\Schemas\Schema;
use Filament\Widgets\ChartWidget\Concerns\HasFiltersSchema;

class BlogPostsChart extends ChartWidget
{
    use HasFiltersSchema;

    // ...

    public function filtersSchema(Schema $schema): Schema
    {
        return $schema->components([
            DatePicker::make('startDate')
                ->default(now()->subDays(30)),
            DatePicker::make('endDate')
                ->default(now()),
        ]);
    }
}
```

- Filter values are accessible through `$this->filters`:

```php
protected function getData(): array
{
    $startDate = $this->filters['startDate'] ?? null;
    $endDate = $this->filters['endDate'] ?? null;

    return [
        // ...
    ];
}
```

- The docs state `$this->filters` always reflects the current form data.
- The docs state this data is not validated because it is live and not intended for anything other than querying the database; ensure it is valid before using it.
- For filters that apply to multiple widgets at once, see dashboard filtering in [overview-dashboard.md](./overview-dashboard.md).

## Deferred Custom Filters
- By default, filters using `filtersSchema()` update chart data immediately when changed.
- Set `$hasDeferredFilters` to `true` to apply filter changes only when the user clicks the Apply button:

```php
use Filament\Widgets\ChartWidget\Concerns\HasFiltersSchema;

class BlogPostsChart extends ChartWidget
{
    use HasFiltersSchema;

    protected bool $hasDeferredFilters = true;

    // ...
}
```

- For dynamic control, override `hasDeferredFilters()`:

```php
public function hasDeferredFilters(): bool
{
    return auth()->user()->prefersDeferredFilters();
}
```

- When using deferred filters, a Reset link appears in the filter dropdown footer alongside the Apply button.
- Reset restores default values defined in `filtersSchema()`.

## Filter Actions
- Deferred filter apply and reset actions can be customized.
- The docs state methods available to customize action trigger buttons can be used.

```php
use Filament\Actions\Action;

public function filtersApplyAction(Action $action): Action
{
    return $action
        ->label('Update Chart')
        ->color('success');
}

public function filtersResetAction(Action $action): Action
{
    return $action
        ->label('Clear Filters')
        ->color('danger');
}
```

## Polling
- By default, chart widgets refresh their data every 5 seconds.
- Customize polling with `$pollingInterval`:

```php
protected ?string $pollingInterval = '10s';
```

- Disable polling with:

```php
protected ?string $pollingInterval = null;
```

## Maximum Height
- Set a maximum chart height with `$maxHeight`:

```php
protected ?string $maxHeight = '300px';
```

## Chart Options
- Chart.js configuration options can be set with `$options`:

```php
protected ?array $options = [
    'plugins' => [
        'legend' => [
            'display' => false,
        ],
    ],
];
```

- Dynamic options can be returned from `getOptions()`:

```php
protected function getOptions(): array
{
    return [
        'plugins' => [
            'legend' => [
                'display' => false,
            ],
        ],
    ];
}
```

- `getOptions()` may return a `RawJs` object for raw JavaScript, such as a JavaScript callback:

```php
use Filament\Support\RawJs;

protected function getOptions(): RawJs
{
    return RawJs::make(<<<JS
        {
            scales: {
                y: {
                    ticks: {
                        callback: (value) => '€' + value,
                    },
                },
            },
        }
    JS);
}
```

## Description
- Add a description below the chart heading with `getDescription()`:

```php
public function getDescription(): ?string
{
    return 'The number of blog posts published per month.';
}
```

## Lazy Loading
- By default, widgets are lazy-loaded and only load when visible on the page.
- Disable lazy loading with:

```php
protected static bool $isLazy = false;
```

## Collapsible Charts
- Make a chart collapsible with `$isCollapsible`:

```php
protected bool $isCollapsible = true;
```

## Custom Chart.js Plugins
- Chart.js plugins can be used in chart widgets.
- Step 1: install a plugin with NPM, such as:

```bash
npm install chartjs-plugin-datalabels --save-dev
```

- Step 2: create a JavaScript file such as `filament-chart-js-plugins.js`, import the plugin, initialize `window.filamentChartJsPlugins`, and push the plugin:

```js
import ChartDataLabels from 'chartjs-plugin-datalabels'

window.filamentChartJsPlugins ??= []
window.filamentChartJsPlugins.push(ChartDataLabels)
```

- Global plugins can be registered with `window.filamentChartJsGlobalPlugins`:

```js
import ChartDataLabels from 'chartjs-plugin-datalabels'

window.filamentChartJsGlobalPlugins ??= []
window.filamentChartJsGlobalPlugins.push(ChartDataLabels)
```

- Step 3: include the JavaScript file in Vite input, then build it with `npm run build`:

```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: [
                'resources/css/app.css',
                'resources/js/app.js',
                'resources/css/filament/admin/theme.css',
                'resources/js/filament-chart-js-plugins.js',
            ],
        }),
    ],
});
```

- Step 4: register the JavaScript file in Filament, for example in a service provider `boot()` method:

```php
use Filament\Support\Assets\Js;
use Filament\Support\Facades\FilamentAsset;
use Illuminate\Support\Facades\Vite;

FilamentAsset::register([
    Js::make('chart-js-plugins', Vite::asset('resources/js/filament-chart-js-plugins.js'))->module(),
]);
```

- The docs mention asset registration and registering assets for a specific panel as related topics; query Context7 for those pages before adding details.
