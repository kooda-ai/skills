---
name: filament-5-widgets
description: 'Use when: working with Filament 5 Widgets, make:filament-widget, dashboard widgets, StatsOverviewWidget, Stat::make(), ChartWidget, table widgets, custom widgets, widget sorting, column spans, dashboard grids, page filters, FilterAction, canView(), polling, lazy loading, chart filters, Chart.js options, and dashboard customization. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Widget task, dashboard widget, stats overview, chart widget, table widget, custom widget, filters, or code to review'
---

# Filament 5 Widgets

## Purpose
Use this skill to create, review, or explain Filament 5 Widgets using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Widgets topic.
2. Do not add behavior, APIs, options, namespaces, commands, properties, Chart.js configuration, Livewire behavior, dashboard routing, or conventions unless they appear in the retrieved documentation.
3. If a requested Widgets topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Widgets tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, property names, namespaces, command flags, and class names.

## Reference Map
- Widget creation, dashboard page customization, dashboard grids, widget widths, visibility, filters, table widgets, custom widgets, and disabling default widgets: [overview-dashboard.md](./references/overview-dashboard.md)
- Stats overview widgets, `StatsOverviewWidget`, `Stat::make()`, stat descriptions, icons, colors, charts, attributes, polling, lazy loading, headings, and descriptions: [stats-overview.md](./references/stats-overview.md)
- Chart widgets, `ChartWidget`, chart data, chart types, colors, model trends, filters, polling, max height, options, descriptions, lazy loading, collapsible charts, and Chart.js plugins: [charts.md](./references/charts.md)

## Workflow
1. Identify the widget context: dashboard widget, stats overview widget, chart widget, table widget, custom widget, dashboard grid/layout, dashboard filter, or widget review.
2. Run a narrow Context7 query for the exact Widgets topic before producing code.
3. Load the relevant reference file from the map above.
4. Use only documented widget generation commands and flags confirmed for the task: `php artisan make:filament-widget MyWidget`, `--stats-overview`, `--chart`, and `--table`.
5. For dashboard registration and defaults, use only documented `Panel` methods and examples such as `widgets([])`, `widgets([...])`, `discoverPages()`, and `pages([...])` when confirmed by the current lookup.
6. For layout, use only documented dashboard `getColumns()` values and widget `$columnSpan` values confirmed by the current lookup.
7. For visibility and ordering, use only documented `$sort` and `canView()` patterns confirmed by the current lookup.
8. For dashboard-wide filters, include `HasFiltersForm`, `filtersForm(Schema $schema): Schema`, `InteractsWithPageFilters`, `HasFiltersAction`, `FilterAction`, `getHeaderActions()`, `$persistsFiltersInSession`, and `persistsFiltersInSession()` only when confirmed by the current lookup.
9. For stats overview widgets, include only documented `StatsOverviewWidget` and `Stat` methods confirmed by the current lookup.
10. For chart widgets, include only documented `ChartWidget` properties, methods, filters, and Chart.js plugin setup confirmed by the current lookup.
11. For table widgets, use this skill only for widget creation and dashboard integration; load the Filament 5 Tables skill for table internals after a Context7 lookup confirms the table task.
12. Finish by checking that every command, class, method, property, trait, import, option, and callback in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- Filament dashboards are comprised of widgets that display data as stats, charts, tables, or custom views.
- `php artisan make:filament-widget MyWidget` creates a widget and asks for the widget type.
- Documented widget type choices are Custom, Chart, Stats overview, and Table.
- Stats overview widgets can be generated with `php artisan make:filament-widget StatsOverview --stats-overview`.
- Chart widgets can be generated with `php artisan make:filament-widget BlogPostsChart --chart`.
- Table widgets can be generated with `php artisan make:filament-widget LatestOrders --table`.
- A widget class can use `protected static ?int $sort = 2;` to change its order on the page relative to other widgets.
- A widget can override `public static function canView(): bool` to conditionally hide itself.
- A custom dashboard page can extend `Filament\Pages\Dashboard as BaseDashboard`.
- A custom dashboard page can override `getColumns(): int | array` for widget grid columns.
- A widget can use `protected int | string | array $columnSpan = 'full';` or a responsive array such as `['md' => 2, 'xl' => 3]` for widget width.
- Default dashboard widgets can be disabled with `widgets([])` in panel configuration.
- Custom widgets create a widget class in the `/Widgets` directory and a Blade view in the `/widgets` directory of the Filament views directory; the class is a Livewire component.
- Dashboard-wide filter form data is available in widgets through `InteractsWithPageFilters` and `$this->pageFilters`, and the docs state this raw form data must be validated before use.
- Dashboard filter action modal data is handled like the filters header form, except the data is validated before being passed to the widget.
- Stats overview widgets extend `StatsOverviewWidget` and return `Stat` instances from `getStats()`.
- Chart widgets extend `ChartWidget`, return datasets and labels from `getData()`, and return the chart type string from `getType()`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each command, class, method, property, trait, import, chart option, filter option, and widget placement choice is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, Laravel habits, Livewire habits, Chart.js habits, or package source code.
- If the user asks for a Widgets topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, static properties, route strings, command flags, and option names intact.
