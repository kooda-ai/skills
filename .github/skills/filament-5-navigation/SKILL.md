---
name: filament-5-navigation
description: 'Use when: working with Filament 5 Navigation, panel navigation, navigation(), NavigationBuilder, NavigationItem, navigationItems(), NavigationGroup, navigationGroups(), topNavigation(), sidebar navigation, breadcrumbs, subNavigationPosition(), Resource or Page navigation labels, icons, active icons, groups, parent items, sort order, badges, hidden navigation items, custom navigation, getNavigationItems(), record sub-navigation, and clusters. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Navigation task, PanelProvider code, Resource/Page navigation code, group/sidebar/topbar setup, or code to review'
---

# Filament 5 Navigation

## Purpose
Use this skill to create, review, or explain Filament 5 navigation using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Navigation topic.
2. Do not add behavior, APIs, options, namespaces, route names, icon values, enum values, static properties, methods, or conventions unless they appear in the retrieved documentation.
3. If a requested Navigation topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Keep navigation examples close to documented snippets and preserve documented class names, method names, static property names, argument names, imports, and enum names.
5. Separate panel-level navigation configuration from Resource/Page navigation configuration before writing code.

## Reference Map
- Panel navigation, navigation builders, custom navigation items, custom groups, and generated navigation items: [panel-navigation.md](./references/panel-navigation.md)
- Resource and Page navigation labels, icons, groups, parent items, sort order, badges, and hidden items: [resource-page-navigation.md](./references/resource-page-navigation.md)
- Sidebar, top navigation, breadcrumbs, and sub-navigation position: [layout-sub-navigation.md](./references/layout-sub-navigation.md)

## Workflow
1. Identify the navigation surface: panel provider navigation, custom links, navigation groups, Resource navigation item, Page navigation item, record sub-navigation, sidebar/top navigation layout, breadcrumbs, or clusters.
2. Run a narrow Context7 query for the exact topic before producing code.
3. Load the relevant reference file from the map above.
4. For panel provider work, use only documented panel methods and navigation classes confirmed for the task, such as `navigation()`, `navigationItems()`, `navigationGroups()`, `NavigationBuilder`, `NavigationItem`, `NavigationGroup`, `topNavigation()`, `breadcrumbs(false)`, and `subNavigationPosition()`.
5. For Resource or Page navigation work, use only documented static properties and methods confirmed for the task, such as `$navigationLabel`, `getNavigationLabel()`, `$navigationIcon`, `$activeNavigationIcon`, `$navigationGroup`, `$navigationParentItem`, `$navigationSort`, `getNavigationBadge()`, `getNavigationBadgeColor()`, `$navigationBadgeTooltip`, `getNavigationBadgeTooltip()`, `$shouldRegisterNavigation`, and `shouldRegisterNavigation()`.
6. For full custom navigation, preserve documented `NavigationBuilder` patterns and use `getNavigationItems()` only for Resources or Pages confirmed by the lookup.
7. For nested navigation, confirm whether the docs require a matching `$navigationGroup` for the child item when `$navigationParentItem` targets a grouped parent.
8. For record sub-navigation, confirm `getRecordSubNavigation(Page $page): array` and `$page->generateNavigationItems([...])` before using them.
9. For clusters, include only the behavior confirmed by the current lookup. If the lookup only confirms that clusters register navigation items automatically, do not add cluster implementation details.
10. Finish by checking that every command, class, method, property, enum, import, route helper, and argument in the answer is traceable to the current Context7 result and the loaded reference file.

## Confirmed Core Patterns
- Filament automatically registers navigation items for resources, custom pages, and clusters.
- Custom navigation items can be registered with `navigationItems()` and `Filament\Navigation\NavigationItem`.
- Full custom navigation can be built with `navigation(function (NavigationBuilder $builder): NavigationBuilder { ... })`.
- Custom navigation groups can be configured with `navigationGroups()` and `Filament\Navigation\NavigationGroup`.
- Resource navigation labels, icons, active icons, groups, parent items, sort order, badges, badge colors, badge tooltips, and hiding from navigation are documented navigation concerns.
- Record sub-navigation is documented through `getRecordSubNavigation(Page $page): array` and `$page->generateNavigationItems([...])`.
- Panel layout navigation concerns include top navigation, sidebar behavior, breadcrumbs, and `subNavigationPosition()` when confirmed by the current lookup.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Panel configuration, Resource configuration, Page configuration, and record sub-navigation are not mixed together unless the docs show the same API for that surface.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, Laravel habits, Livewire habits, package source code, or memory.
- If the user asks for a navigation topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, static properties, enum names, route helpers, and argument names intact.