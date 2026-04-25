---
name: filament-5-infolists
description: 'Use when: working with Filament 5 Infolists, infolist(Schema $schema), Resource infolist schemas, reusable CustomerInfolist-style schema classes, Infolists package overview, TextEntry, IconEntry, ImageEntry, ColorEntry, CodeEntry, KeyValueEntry, RepeatableEntry, custom entries, entry formatting, badges, visibility, schema layouts, Grid, Section, Tabs, and entry utility injection. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Infolist task, Resource infolist, entry component, layout, formatting, visibility, or code to review'
---

# Filament 5 Infolists

## Purpose
Use this skill to create, review, or explain Filament 5 Infolists using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Infolists topic.
2. Do not add behavior, APIs, options, namespaces, commands, entry methods, layout methods, action methods, or conventions unless they appear in the retrieved documentation.
3. If a requested Infolists topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Infolists tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, utility names, and component class names.

## Reference Map
- Package purpose, Resource `infolist()` delegation, reusable infolist schema classes, and confirmed setup boundaries: [setup-resource.md](./references/setup-resource.md)
- Built-in entry types, `TextEntry` formatting, badge/color examples, and entry utility injection: [entries-text.md](./references/entries-text.md)
- Schema layouts, `hidden()` and `visible()`, responsive columns, tabs, and unconfirmed action/layout boundaries: [layouts-visibility.md](./references/layouts-visibility.md)

## Workflow
1. Identify the Infolists context: package overview, Resource `infolist()`, reusable infolist schema class, entry component, `TextEntry` formatting, layout, visibility, or entry utility injection.
2. Run a narrow Context7 query for the exact Infolists topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented schema entry points confirmed for the task, such as `infolist(Schema $schema): Schema`, `configure(Schema $schema): Schema`, `components()`, and `schema()`.
5. Add infolist entries only from documented entry types and methods confirmed by the current lookup.
6. For Resource infolists, use `public static function infolist(Schema $schema): Schema` and delegate to a reusable schema class only when the current lookup confirms that pattern.
7. For `TextEntry` work, use only documented methods such as `make()`, `dateTime()`, `badge()`, `color()`, `formatStateUsing()`, `words()`, and `numeric()` when confirmed by the current lookup.
8. For layout work, use only documented schema layout components and methods such as `Grid::make(2)`, `Section::make(...)->schema([...])`, `columns()`, `columnSpan()`, `columnOrder()`, `Tabs::make()`, `tabs()`, and `Tab::make(...)->schema([...])` when confirmed by the current lookup.
9. For visibility, use `hidden()` or `visible()` only when the current lookup confirms the relevant condition pattern.
10. For entry utility injection, use only the documented injectable parameters returned by the lookup.
11. Finish by checking that every method, class, import, option, and utility parameter in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- The Infolists package displays a read-only list of data for a specific entity.
- The docs state that Infolists integrate into panel resources, relation managers, and action modals.
- A Resource infolist can use `public static function infolist(Schema $schema): Schema` and delegate to `CustomerInfolist::configure($schema)`.
- A reusable infolist schema class can follow the documented reusable schema pattern with `public static function configure(Schema $schema): Schema` when the current lookup confirms it for the task.
- The docs show `Filament\Schemas\Schema` as the schema type for Resource `infolist()`.
- The docs show `Filament\Infolists\Components\TextEntry` inside schema components.
- The docs mention built-in entry types for text, icon, image, color, code, key-value, and repeatable entries, plus custom entries.
- Confirmed `TextEntry` methods from the retrieved docs include `make()`, `dateTime()`, `badge()`, `color()`, `formatStateUsing()`, `words()`, and `numeric()`.
- Confirmed visibility methods for an infolist entry include `hidden()` and `visible()`.
- Confirmed schema layout components and methods around infolist entries include `Grid`, `Section`, `Tabs`, `Tab`, `schema()`, `columns()`, `columnSpan()`, `columnOrder()`, and `tabs()`.
- Confirmed entry utility injection parameters include `$component`, `$get`, `$model`, `$livewire`, `$state`, `$operation`, and `$record`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each class, method, import, option, and utility parameter is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, general Laravel habits, or package source code.
- If the user asks for an Infolists topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, schema structure, and utility names intact.
