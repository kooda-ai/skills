---
name: filament-5-schemas
description: 'Use when: working with Filament 5 Schemas, Schema classes, form schemas, infolist schemas, Livewire HasSchemas and InteractsWithSchemas, Resource form() and infolist(), components(), statePath(), fill(), getState(), Grid, Section, Tabs, Builder blocks, schema utility injection, and actions inside schemas. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Schema task, form/infolist schema, Livewire component, Resource schema, or code to review'
---

# Filament 5 Schemas

## Purpose
Use this skill to create, review, or explain Filament 5 Schemas using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Schemas topic.
2. Do not add behavior, APIs, options, namespaces, commands, or conventions unless they appear in the retrieved documentation.
3. If a requested Schemas topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split long Schemas topics into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names and namespaces.

## Reference Map
- Schema setup, Livewire components, Resource schema methods, and reusable schema classes: [schema-setup.md](./references/schema-setup.md)
- Documented schema components, layout components, tabs, and builder blocks: [components-layouts.md](./references/components-layouts.md)
- State handling, utility injection, and actions inside schemas: [state-actions-utilities.md](./references/state-actions-utilities.md)

## Workflow
1. Identify the schema context: Livewire form component, Resource `form()`, Resource `infolist()`, reusable schema class, or schema component review.
2. Run a narrow Context7 query for the exact Schemas topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented schema entry points confirmed for the task: `form(Schema $schema): Schema`, `infolist(Schema $schema): Schema`, `configure(Schema $schema): Schema`, `components()`, `schema()`, `statePath()`, `fill()`, and `getState()`.
5. Add components only from documented component classes and methods confirmed by the current lookup.
6. For Livewire schema usage, include `HasSchemas`, `InteractsWithSchemas`, a nullable array state property when using `statePath('data')`, and `fill()` only when confirmed by the current lookup.
7. For actions inside schemas, use only documented schema action utilities such as `$schemaGet` and `$schemaSet` when the current lookup confirms them.
8. Finish by checking that every method, class, import, and option in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- A Livewire component using Filament schemas implements `HasSchemas` and uses `InteractsWithSchemas`.
- A form schema method can accept and return `Filament\Schemas\Schema`.
- A Livewire form schema can define components with `components([...])` and store state with `statePath('data')`.
- The docs show `mount()` calling `$this->form->fill()` and a submit method reading `$this->form->getState()`.
- Resource schema methods can delegate to reusable classes through `CustomerForm::configure($schema)` and `CustomerInfolist::configure($schema)`.
- A reusable schema class can expose `public static function configure(Schema $schema): Schema`.
- Layout components shown in the retrieved docs include `Grid`, `Section`, `Tabs`, and `Tabs\Tab`.
- Form/input components shown in the retrieved docs include `TextInput`, `MarkdownEditor`, `Checkbox`, `Select`, `Builder`, `Builder\Block`, `FileUpload`, and `Textarea`.
- Infolist entry components shown in the retrieved docs include `TextEntry`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each class, method, import, and option is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, or general Laravel knowledge.
- If the user asks for a topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces and method names intact.