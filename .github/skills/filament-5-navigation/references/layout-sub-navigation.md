# Layout And Sub-navigation

Use this reference only after a fresh Context7 lookup for `/websites/filamentphp_5_x` confirms the relevant Filament 5 navigation layout, sidebar, topbar, breadcrumbs, or sub-navigation topic.

## Sidebar And Top Navigation
- The docs state that Filament uses sidebar navigation by default.
- When confirmed by the current lookup, use `topNavigation()` for top navigation.
- When confirmed by the current lookup, use `sidebarCollapsibleOnDesktop()` for a collapsible desktop sidebar.
- When confirmed by the current lookup, use `sidebarFullyCollapsibleOnDesktop()` for a fully collapsible desktop sidebar.
- When confirmed by the current lookup, use `sidebarWidth('40rem')` to customize sidebar width.
- When confirmed by the current lookup, use `collapsedSidebarWidth('9rem')` with a collapsible sidebar to customize collapsed sidebar width.
- When confirmed by the current lookup, use `topbar(false)` to disable the topbar.

## Breadcrumbs
- When confirmed by the current lookup, use `breadcrumbs(false)` to disable breadcrumbs.

## Panel-wide Sub-navigation Position
When confirmed by the current lookup, set the panel-wide sub-navigation position with `subNavigationPosition()`.

```php
use Filament\Pages\Enums\SubNavigationPosition;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->subNavigationPosition(SubNavigationPosition::End);
}
```

Previously retrieved docs confirmed `Filament\Pages\Enums\SubNavigationPosition` values `SubNavigationPosition::Start`, `SubNavigationPosition::End`, and `SubNavigationPosition::Top`.

## Record Sub-navigation Relationship
- Use this file for panel-wide sub-navigation position only.
- Use [resource-page-navigation.md](./resource-page-navigation.md) for Resource record sub-navigation with `getRecordSubNavigation(Page $page): array` and `$page->generateNavigationItems([...])`.

## Not Confirmed In Current Lookup
Do not add custom sidebar/topbar Livewire component replacement, sidebar refresh events, menu item APIs, or cluster implementation details unless a narrower Context7 lookup returns them.