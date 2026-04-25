---
name: filament-5-testing
description: 'Use when: working with Filament 5 Testing, Livewire component tests, Pest livewire(), PHPUnit Livewire::test(), testing Resources and pages, create/edit forms, validation, table records, table filters, table columns, actions, table actions with TestAction, notifications, and documented authorization-related test context. Requires Context7 Filament 5.x docs before adding details.'
argument-hint: 'Testing task, Resource page, Livewire component, table test, schema/form test, action test, notification test, or code to review'
---

# Filament 5 Testing

## Purpose
Use this skill to create, review, or explain Filament 5 tests using only details confirmed in the Filament 5.x documentation from Context7.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/websites/filamentphp_5_x` with the exact Testing topic.
2. Do not add testing helpers, namespaces, assertions, method signatures, commands, policy behavior, Livewire behavior, or conventions unless they appear in the retrieved documentation.
3. If a requested Testing topic is not confirmed by the retrieved docs, say that the current documentation context did not confirm it and either run a narrower Context7 lookup or leave the topic out.
4. Split broad Testing tasks into reference-backed sections instead of guessing or compressing undocumented details.
5. Keep examples close to documented snippets and preserve documented method names, namespaces, callback parameters, and component class names.

## Reference Map
- Testing overview, Livewire basis, Pest/PHPUnit choice, Resource pages, create/edit forms, validation, and table filtering in Resources: [overview-resources.md](./references/overview-resources.md)
- Testing Tables and Schemas, including table records, filters, columns, `fillForm()`, and schema state assertions: [tables-schemas.md](./references/tables-schemas.md)
- Testing Actions, table actions with `TestAction`, notifications, and documented authorization context: [actions-notifications-authorization.md](./references/actions-notifications-authorization.md)

## Workflow
1. Identify the test target: Filament component, Resource page, create/edit form, validation path, table records, table filter, table column, schema state, action, table action, notification, or authorization-related behavior.
2. Run a narrow Context7 query for the exact Filament 5.x Testing topic before producing code.
3. Load the relevant reference file from the map above.
4. Use Filament's documented testing basis: Filament components are tested through Livewire testing helpers; examples use Pest's `livewire()` function and can be adapted to PHPUnit with `Livewire::test()` when the docs confirm that note.
5. For Resource page tests, use only documented page classes and helpers confirmed by the current lookup, such as `livewire(ListUsers::class)`, `livewire(EditUser::class, ['record' => $user->id])`, `fillForm()`, `call('save')`, `assertHasFormErrors()`, `assertNotified()`, and `assertNotNotified()`.
6. For table tests, use only documented helpers confirmed by the lookup, such as `assertCanSeeTableRecords()`, `assertCanNotSeeTableRecords()`, `filterTable()`, and `assertTableColumnExists()`.
7. For schema and form tests, use only documented helpers confirmed by the lookup, such as `fillForm()` and `assertSchemaStateSet()`.
8. For action tests, use only documented helpers confirmed by the lookup, such as `callAction()`, `Filament\Actions\Testing\TestAction`, `TestAction::make()`, `table()`, `assertActionVisible()`, and `assertActionExists()`.
9. For notification checks, use only documented helpers confirmed by the lookup, such as `assertNotified()` and `assertNotNotified()`.
10. For authorization-related testing context, only mention documented `authorize()` usage or built-in panel Resource policy handling when the current lookup confirms it; do not invent policy tests or permission setup.
11. Finish by checking that every helper, assertion, class, namespace, callback argument, page parameter, and action target in the answer is present in the Context7 result used for the task.

## Confirmed Core Patterns
- Filament testing utilities leverage Livewire testing helpers because Filament components are mounted to Livewire components.
- Filament testing examples use Pest's `livewire()` function.
- The docs state that tests can be adapted for PHPUnit by replacing Pest's `livewire()` function with Livewire's `Livewire::test()` method.
- The docs confirm testing guides for panel Resources, Tables, Schemas, Actions, and sent Notifications.
- Confirmed Resource and form testing helpers from the retrieved docs include `fillForm()`, `call('save')`, `assertHasFormErrors()`, `assertNotified()`, and `assertNotNotified()`.
- Confirmed table testing helpers from the retrieved docs include `assertCanSeeTableRecords()`, `assertCanNotSeeTableRecords()`, `filterTable()`, and `assertTableColumnExists()`.
- Confirmed schema testing helpers from the retrieved docs include `fillForm()` and `assertSchemaStateSet()`.
- Confirmed action testing helpers from the retrieved docs include `callAction()`, `TestAction::make()`, `table()`, `assertActionVisible()`, and `assertActionExists()`.
- Confirmed notification testing helpers from the retrieved docs include `assertNotified()` and `assertNotNotified()`.
- Confirmed authorization context from the retrieved docs includes `Action::make(...)->authorize('update')` and the note that Filament automatically handles policies for built-in actions in panel Resources.

## Completion Check
- The answer uses only APIs and examples confirmed by the current Context7 lookup.
- Each helper, assertion, class, namespace, page parameter, callback, and action target is traceable to the retrieved Filament 5.x docs.
- Unconfirmed topics are not inferred from Filament 4.x, older examples, memory, Laravel habits, Livewire habits, Pest habits, or package source code.
- If the user asks for a Testing topic not present in the Context7 result, run a narrower lookup or explicitly leave it out.
- Code examples keep documented namespaces, method names, page constructor parameters, action names, and callback signatures intact.