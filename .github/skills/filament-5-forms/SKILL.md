---
name: filament-5-forms
description: 'Use when: working with Filament 5 Forms, form(Schema $schema), standalone Livewire forms, Resource form schemas, TextInput, Select, Checkbox, Toggle, MarkdownEditor, RichEditor, FileUpload, Repeater, Builder, dynamic dependent fields, validation rules, hidden fields, field state updates, createOptionForm(), relationship(), schema actions, Get and Set utilities. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Form task, Resource form, Livewire form, field component, validation, state update, or code to review'
---

# Filament 5 Forms

## Purpose
Use this skill to create, review, or explain Filament 5 Forms using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Forms topic.
2. Do not add behavior, APIs, options, namespaces, commands, validation rules, relationship behavior, lifecycle hooks, or conventions unless they appear in the retrieved documentation.
3. If a requested Forms topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Forms tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, utility names, and component class names.

## Reference Map
- Standalone Livewire forms, Resource form delegation, reusable form schema classes, `components()`, `statePath()`, `fill()`, and `getState()`: [form-setup.md](./references/form-setup.md)
- Confirmed form components, Select options, multiple Select, BelongsTo Select relationships, create-option modal forms, and dynamic dependent fields: [fields-select-dynamic.md](./references/fields-select-dynamic.md)
- Repeater, Builder, RichEditor, Toggle, and related item/action controls confirmed by Context7: [complex-editor-components.md](./references/complex-editor-components.md)
- Validation closure rules, `Get` and `Set` utilities, `live()`, `afterStateUpdated()`, and actions inside schemas: [validation-state-actions.md](./references/validation-state-actions.md)

## Workflow
1. Identify the Forms context: standalone Livewire form, Resource `form()`, reusable form schema class, individual form field, validation rule, dependent field, Select relationship, or schema action.
2. Run a narrow Context7 query for the exact Forms topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented form entry points confirmed for the task: `form(Schema $schema): Schema`, `configure(Schema $schema): Schema`, `components()`, `statePath()`, `fill()`, and `getState()`.
5. Add form components only from documented component classes and methods confirmed by the current lookup.
6. For standalone Livewire forms, include `HasSchemas`, `InteractsWithSchemas`, a nullable array state property, `statePath('data')`, `mount()` calling `$this->form->fill()`, and submit handling through `$this->form->getState()` only when confirmed by the current lookup.
7. For Resource forms, use `public static function form(Schema $schema): Schema` and delegate to a reusable schema class only when that pattern is confirmed.
8. For dynamic or dependent fields, use only documented utilities and hooks such as `Get`, `Set`, `live()`, `afterStateUpdated()`, `schema(fn (Get $get): array => ...)`, and keyed child schemas when confirmed.
9. For Select relationships and option creation, use only documented `relationship(name: ..., titleAttribute: ...)`, `multiple()`, `options()`, and `createOptionForm()` patterns confirmed by the lookup.
10. For Repeater and Builder work, load the complex component reference and only use documented item labels, relationship integration, block definitions, extra item actions, and delete/reorder controls confirmed by the lookup.
11. Finish by checking that every method, class, import, option, validation call, and utility parameter in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- A standalone Livewire form component implements `Filament\Schemas\Contracts\HasSchemas` and uses `Filament\Schemas\Concerns\InteractsWithSchemas`.
- A standalone form can define `public ?array $data = [];`, call `$this->form->fill()` in `mount()`, configure a `form(Schema $schema): Schema`, and read submitted state with `$this->form->getState()`.
- A form schema can use `$schema->components([...])->statePath('data')`.
- A Resource form can use `public static function form(Schema $schema): Schema` and delegate to `CustomerForm::configure($schema)`.
- A reusable form schema class can expose `public static function configure(Schema $schema): Schema`.
- Confirmed form component classes from the retrieved docs include `TextInput`, `MarkdownEditor`, `RichEditor`, `Select`, `Checkbox`, `Toggle`, `FileUpload`, `Repeater`, `Builder`, and `Builder\Block`.
- Confirmed schema layout components used around forms include `Grid` and `Section`.
- Confirmed field methods from the retrieved docs include `make()`, `required()`, `options()`, `multiple()`, `relationship()`, `createOptionForm()`, `live()`, `afterStateUpdated()`, `numeric()`, `prefix()`, `image()`, `email()`, `rules()`, `hidden()`, `schema()`, `columns()`, `itemLabel()`, `blocks()`, `extraItemActions()`, `getItemState()`, `reorderable(false)`, and `deletable(false)`.
- The docs confirm dynamic fields by passing a `fn (Get $get): array => ...` callback to `schema()` on a layout component, using `Select::make(...)->live()`, and using `afterStateUpdated()` to fill a keyed child schema.
- The docs confirm closure validation rules using `Filament\Schemas\Components\Utilities\Get` inside `rules()`.
- The docs confirm schema actions with `Filament\Actions\Action`, `afterContent()`, and utility injection using `Get $schemaGet` and `Set $schemaSet`.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each class, method, import, validation call, utility, and option is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, Laravel habits, or package source code.
- If the user asks for a Forms topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, state paths, utility names, and component names intact.