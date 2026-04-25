---
name: filament-5-actions
description: 'Use when: working with Filament 5 Actions, Action::make(), BulkAction, BulkActionGroup, CreateAction, DeleteAction, ForceDeleteAction, RestoreAction, action modals, modal footer actions, sticky modal footers, action lifecycle hooks, table recordActions(), toolbarActions(), schema actions, notification actions, and action utility injection. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Action task, table action, bulk action, modal action, schema action, notification action, or code to review'
---

# Filament 5 Actions

## Purpose
Use this skill to create, review, or explain Filament 5 Actions using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Actions topic.
2. Do not add behavior, APIs, options, namespaces, commands, lifecycle hooks, modal options, authorization rules, transaction behavior, testing helpers, or conventions unless they appear in the retrieved documentation.
3. If a requested Actions topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Actions tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, utility names, and component class names.

## Reference Map
- Livewire action setup, `HasActions`, `InteractsWithActions`, and action utility injection: [setup-utilities.md](./references/setup-utilities.md)
- Modals, extra modal footer actions, sticky modal footers, CreateAction lifecycle hooks, cancellation, and notification actions: [modals-lifecycle-notifications.md](./references/modals-lifecycle-notifications.md)
- Table record actions, toolbar actions, bulk action groups, soft-delete actions, and schema actions: [tables-schemas-resources.md](./references/tables-schemas-resources.md)

## Workflow
1. Identify the Actions context: standalone Livewire action support, table record action, toolbar action, bulk action, Resource table action, Resource page header action, schema action, modal action, lifecycle hook, or notification action.
2. Run a narrow Context7 query for the exact Actions topic before producing code.
3. Load the relevant reference file from the map above.
4. Choose only documented action entry points confirmed for the task: `Action::make()`, `BulkAction::make()`, `BulkActionGroup::make()`, `CreateAction::make()`, `DeleteAction::make()`, `ForceDeleteAction::make()`, `RestoreAction::make()`, `DeleteBulkAction::make()`, `ForceDeleteBulkAction::make()`, and `RestoreBulkAction::make()`.
5. For standalone Livewire action support, include `HasActions`, `InteractsWithActions`, `HasSchemas`, and `InteractsWithSchemas` only when the current lookup confirms the component setup.
6. For table actions, use only documented placement methods such as `recordActions()` and `toolbarActions()` confirmed by the current lookup.
7. For bulk actions, use only documented `BulkAction`, `BulkActionGroup`, `$selectedRecords`, and collection callback patterns confirmed by the current lookup.
8. For action modals, include only documented modal methods confirmed by the lookup, such as `requiresConfirmation()`, `modalIcon()`, `modalHeading()`, `extraModalFooterActions()`, `makeModalSubmitAction()`, and `stickyModalFooter()`.
9. For lifecycle hooks, include only documented hooks returned by Context7 for that action type. The current reference confirms `CreateAction` hooks: `beforeFormFilled()`, `afterFormFilled()`, `beforeFormValidated()`, `afterFormValidated()`, `before()`, and `after()`.
10. For schema actions, use only documented schema placement and utilities, such as `afterContent()`, `Get $schemaGet`, and `Set $schemaSet`, when confirmed.
11. Finish by checking that every class, method, import, callback parameter, modal option, utility injection, and placement method in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- A Livewire component using actions implements `Filament\Actions\Contracts\HasActions` and `Filament\Schemas\Contracts\HasSchemas`, and uses `Filament\Actions\Concerns\InteractsWithActions` and `Filament\Schemas\Concerns\InteractsWithSchemas`.
- Confirmed action utility injection parameters include `$action`, `$arguments`, `$data`, `$livewire`, `$model`, `$record`, `$selectedRecords`, `$mountedActions`, `$schema`, `$schemaComponent`, `$schemaGet`, `$schemaSet`, `$schemaComponentState`, `$schemaOperation`, `$schemaState`, and `$table`.
- Confirmed action group utility injection parameters include `$group`, `$livewire`, `$model`, `$record`, and `$mountedActions`.
- Confirmed table placements include `recordActions()` for row-specific actions and `toolbarActions()` for toolbar and bulk actions.
- Confirmed custom action methods include `action()`, `hidden()`, `visible()`, `color()`, `icon()`, `modalIcon()`, `modalHeading()`, `requiresConfirmation()`, and `button()`.
- Confirmed modal methods include `extraModalFooterActions()`, `makeModalSubmitAction()`, and `stickyModalFooter()`.
- Confirmed `CreateAction` lifecycle hooks include `beforeFormFilled()`, `afterFormFilled()`, `beforeFormValidated()`, `afterFormValidated()`, `before()`, and `after()`.
- Confirmed cancellation method from the retrieved docs is `$action->cancel()`.
- Confirmed notification action pattern uses `Notification::make()->actions([...])` with `Filament\Actions\Action` instances.
- Confirmed soft-delete table and page action classes include `DeleteAction`, `ForceDeleteAction`, `RestoreAction`, `DeleteBulkAction`, `ForceDeleteBulkAction`, and `RestoreBulkAction`.
- Confirmed schema action pattern embeds `Filament\Actions\Action` with `afterContent()` and can use `Get $schemaGet` and `Set $schemaSet` utilities.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each class, method, import, callback parameter, modal option, lifecycle hook, and utility is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, Laravel habits, or package source code.
- If the user asks for an Actions topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, action placement methods, and utility names intact.