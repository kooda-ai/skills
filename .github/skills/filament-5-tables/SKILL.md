---
name: filament-5-tables
description: 'Use when: working with Filament 5 Tables, table configuration classes, Livewire table components, Resource table() methods, columns, TextColumn, IconColumn, ImageColumn, ColorColumn, editable columns, filters, SelectFilter, TrashedFilter, record actions, toolbar actions, bulk actions, soft-delete table actions, pagination, sorting, custom records, and documented table/action utilities. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Table task, model name, Resource table, Livewire component, or code to review'
---

# Filament 5 Tables

## Purpose
Use this skill to create, review, or explain Filament 5 Tables using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Tables topic.
2. Do not add behavior, APIs, options, namespaces, commands, or conventions unless they appear in the retrieved documentation.
3. If a requested Tables topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split long topics into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names and namespaces.

## Reference Map
- Columns and column utilities: [columns.md](./references/columns.md)
- Filters, actions, bulk actions, and soft-delete actions: [filters-actions.md](./references/filters-actions.md)
- Table setup, Livewire components, custom records, pagination, sorting, and soft deletes: [table-behavior.md](./references/table-behavior.md)

## Workflow
1. Identify the table context: table configuration class, Livewire component table, Resource `table()` method, custom data table, or soft-delete Resource table.
2. Run a narrow Context7 query for the exact topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented table entry points confirmed for the task: `configure(Table $table): Table`, `table(Table $table): Table`, `query()`, `records()`, `columns()`, `filters()`, `recordActions()`, `toolbarActions()`, `searchable()`, `defaultSort()`, and `defaultPaginationPageOption()`.
5. Add columns only from documented column types and options confirmed by the current lookup.
6. Add filters only from documented filter types and options confirmed by the current lookup.
7. Add row and bulk behavior only with documented actions, `recordActions()`, `toolbarActions()`, and `BulkActionGroup`.
8. For soft deletes, include only the documented `TrashedFilter`, delete, force-delete, restore, and route-binding query pieces when relevant.
9. Finish by checking that every method, class, import, and option in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- The docs confirm a `make:filament-table` command for generating table configuration classes, but the retrieved result did not provide a full CLI signature. Do not invent command arguments unless a fresh Context7 result shows them.
- A table configuration class uses `public static function configure(Table $table): Table`.
- A Livewire table component implements `HasActions`, `HasSchemas`, and `HasTable`, and uses `InteractsWithActions`, `InteractsWithSchemas`, and `InteractsWithTable`.
- A Livewire table can use `query(Product::query())` for Eloquent records.
- A table can use `records()` for custom data, including external API data, when the current docs confirm the pattern.
- Row actions belong in `recordActions()`.
- Toolbar and bulk actions belong in `toolbarActions()`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each class, method, command, import, and option is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, or general Laravel knowledge.
- If the user asks for a topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces and method names intact.