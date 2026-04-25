---
name: filament-5-resources
description: 'Use when: working with Filament 5 Resources, Resource classes, make:filament-resource, simple resources, form(), infolist(), table(), getPages(), resource pages, ViewRecord pages, page routes, ListRecords, CreateRecord, EditRecord, ViewRecord, relation managers, relation pages, getRelations(), getRecordSubNavigation(), navigation icons, groups, parent items, sort order, badges, labels, plural model labels, slugs, getUrl(), global search record titles, authorization policies, deleting records, and soft deletes. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Resource task, model name, Resource class, page route, relation manager/page, navigation, or code to review'
---

# Filament 5 Resources

## Purpose
Use this skill to create, review, or explain Filament 5 Resources using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Resources topic.
2. Do not add behavior, APIs, options, namespaces, commands, properties, or conventions unless they appear in the retrieved documentation.
3. If a requested Resources topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Resource tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, route strings, and class names.

## Reference Map
- Resource generation, simple resources, generated structure, Resource form/table/infolist delegation, custom slugs, and URLs: [resource-setup.md](./references/resource-setup.md)
- Resource pages, `getPages()`, page routes, and record sub-navigation: [pages-navigation.md](./references/pages-navigation.md)
- Relation managers, relation pages, labels, and global search record titles: [relationships-search.md](./references/relationships-search.md)
- Authorization policies, deleting records, and soft-delete Resource setup: [authorization-soft-deletes.md](./references/authorization-soft-deletes.md)

## Workflow
1. Identify the Resource task: generating a Resource, customizing navigation or labels, defining page routes, adding record sub-navigation, managing relationships, generating URLs, or reviewing existing Resource code.
2. Run a narrow Context7 query for the exact Resources topic before producing code.
3. Load the relevant reference file from the map above.
4. Use only documented Resource entry points confirmed for the task: `php artisan make:filament-resource Customer`, `--simple`, `--soft-deletes`, `php artisan make:filament-page ViewUser --resource=UserResource --type=ViewRecord`, `form()`, `infolist()`, `table()`, `getUrl()`, `getPages()`, `route()`, `getRelations()`, `getRecordSubNavigation()`, `getRecordRouteBindingEloquentQuery()`, `$slug`, `$navigationIcon`, `$navigationLabel`, `$navigationParentItem`, `$navigationGroup`, `$navigationSort`, `getNavigationBadge()`, `getNavigationBadgeColor()`, `$navigationBadgeTooltip`, `getNavigationBadgeTooltip()`, `$shouldRegisterNavigation`, `shouldRegisterNavigation()`, `$pluralModelLabel`, and `$recordTitleAttribute`.
5. For Resource schema or table internals, use this skill only for the Resource integration point and load the Filament 5 Schemas or Filament 5 Tables skill for the schema/table details.
6. For relationships, choose between a relation manager and a relation page only when the current lookup confirms the requested pattern.
7. For navigation and labels, add only documented static properties or methods confirmed by the current lookup.
8. Finish by checking that every command, class, method, property, import, and route pattern in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- The docs confirm `php artisan make:filament-resource Customer` for creating a Resource for an Eloquent model.
- The docs confirm `php artisan make:filament-resource Customer --simple` for a simple Resource that manages records with modals on a single page.
- The docs state that creating a Resource generates several files, including the main Resource class, Create/Edit/List pages, schemas for forms and infolists, and tables for data display.
- The docs confirm Resource `form(Schema $schema): Schema`, `infolist(Schema $schema): Schema`, and `table(Table $table): Table` methods delegating to dedicated schema/table configuration classes.
- The docs confirm `php artisan make:filament-page ViewUser --resource=UserResource --type=ViewRecord` for adding a View page to an existing Resource, followed by registering the page in `getPages()`.
- The docs confirm `CustomerResource::getUrl()` for generating the Resource List page URL.
- The docs confirm `protected static ?string $slug = 'pending-orders';` for customizing a Resource URL slug.
- The docs confirm `getPages()` route registration with `Pages\ListCustomers::route('/')`, `Pages\CreateCustomer::route('/create')`, `Pages\ViewCustomer::route('/{record}')`, and `Pages\EditCustomer::route('/{record}/edit')`.
- The docs confirm `getRelations()` with relation manager classes.
- The docs confirm relation pages registered in `getPages()`, including a route such as `/{record}/addresses`.
- The docs state that when using a relation page, a separate relation manager does not need to be generated or registered.
- The docs confirm `getRecordSubNavigation(Page $page): array` and `$page->generateNavigationItems([...])` for record sub-navigation.
- The docs confirm `$navigationIcon`, `$navigationLabel`, `$navigationParentItem`, `$navigationGroup`, `$navigationSort`, navigation badges, navigation badge color, navigation badge tooltip, and hiding Resources from navigation.
- The docs confirm `$pluralModelLabel` and `$recordTitleAttribute` static properties.
- The docs confirm Resource authorization through Laravel model policies for listing, editing, deleting, reordering, force-deleting, and restoring records.
- The docs confirm `php artisan make:filament-resource Customer --soft-deletes`, `TrashedFilter`, delete/force-delete/restore actions, related bulk actions, and `getRecordRouteBindingEloquentQuery()` with `SoftDeletingScope` removal for soft-delete Resources.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each command, class, method, property, import, route pattern, and option is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, or general Laravel knowledge.
- If the user asks for a Resource topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, static properties, and route strings intact.