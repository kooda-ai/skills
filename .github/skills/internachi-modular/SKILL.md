---
name: internachi-modular
description: 'Use when: working with InterNACHI Modular, Interachi modular package, internachi/modular, Laravel modules, make:module, modules:cache, modules:clear, modules:sync, modules:list, Composer path repositories for app-modules, module auto-discovery, module stubs, and Laravel make commands with --module. Requires Context7 /internachi/modular docs before adding details.'
argument-hint: 'InterNACHI Modular task, module scaffolding, module command, module structure, Composer path repository, or code to review'
---

# InterNACHI Modular

## Purpose
Use this skill to create, review, or explain InterNACHI Modular package usage for Laravel applications using only details confirmed in the current Context7 documentation for `/internachi/modular`.

## Source Rule
1. Before giving final code or guidance, query Context7 for `/internachi/modular` with the exact topic the user asks about.
2. Do not add installation steps, module paths, Composer keys, commands, config keys, namespaces, package-discovery behavior, generated files, auto-discovery claims, stub placeholders, or make-command coverage unless they appear in the retrieved documentation.
3. If the user asks about behavior not confirmed by the current Context7 result, run a narrower Context7 lookup or explicitly say the current documentation context does not confirm it.
4. Keep examples close to documented snippets and preserve documented command names, Composer keys, package names, module names, placeholders, and paths.
5. Do not infer Laravel package behavior, Composer behavior, testing strategy, file layout details, or service-provider implementation beyond the documented InterNACHI Modular facts.

## Reference Map
- Installation, module generation, Composer path repositories, helper commands, auto-discovery, `--module` make commands, and stub placeholders: [package-reference.md](./references/package-reference.md)

## Workflow
1. Identify the requested surface: package installation, config publishing, new module scaffolding, root Composer update, module command usage, Laravel feature auto-discovery, Laravel `make:` command support, stub placeholders, or code review.
2. Run a narrow Context7 query for `/internachi/modular` before producing code or final guidance.
3. Load the reference file from the map above.
4. For installation, use only the documented Composer command and the documented Laravel auto-discovery setup statement.
5. For configuration, use only the documented publish command and the documented reason: customization of the default module namespace.
6. For module creation, use only the documented `php artisan make:module my-module` example and documented statement that it scaffolds `composer.json`, `src`, `tests`, `routes`, `resources`, and `database` folders and updates the project's `composer.json`.
7. For Composer integration, use only the documented path repository example with `type`, `url`, and `require` entries.
8. For helper commands, list only the documented commands: `make:module`, `modules:cache`, `modules:clear`, `modules:sync`, and `modules:list`. Describe their purpose only at the documented level.
9. For Laravel auto-discovery, list only the documented features: Artisan commands, migrations, factories for `factory()`, policies for models, Blade components, and event listeners.
10. For Laravel generator support, use only the documented `make:* --module=[module name]` commands from the reference file.
11. For stubs, use only the documented placeholder names from the reference file and do not invent placeholder meanings unless the current lookup explains them.
12. For reviews, verify every command, path, package name, Composer key, generated-folder claim, auto-discovery claim, make-command name, and placeholder against the current Context7 result and the reference file.

## Confirmed Core Patterns
- The package is installed with `composer require internachi/modular`.
- The docs state Laravel's auto-discovery handles setup after installation.
- The docs show publishing configuration with `php artisan vendor:publish --tag=modular-config` to customize the default module namespace.
- The docs show creating a module with `php artisan make:module my-module`.
- The docs state module scaffolding includes `composer.json`, `src`, `tests`, `routes`, `resources`, and `database` folders.
- The docs state module creation updates the project's `composer.json` to include the new module.
- The docs show a Composer path repository using `type: path`, `url: ./app-modules/my-module`, and `require` entry `modules/my-module: *`.
- The docs list helper commands for scaffolding, caching, clearing cache, syncing configurations, and listing available modules.
- The docs state modules auto-integrate commands, migrations, factories, policies, Blade components, and event listeners with Laravel features.
- The docs state most Laravel standard `make:` commands are extended with `--module=[module name]` and leverage existing Laravel tooling and custom stubs.
- The docs list module generation placeholders including `StubBasePath`, `StubModuleNamespace`, `StubComposerNamespace`, `StubModuleNameSingular`, `StubModuleNamePlural`, `StubModuleName`, `StubClassNamePrefix`, `StubComposerName`, `StubMigrationPrefix`, `StubFullyQualifiedTestCaseBase`, and `StubTestCaseBase`.

## Completion Check
- A fresh Context7 lookup for `/internachi/modular` was performed for the user's exact topic.
- Every included command, Composer field, package name, path, generated-folder statement, auto-discovery feature, make-command example, and stub placeholder is confirmed by the current lookup or by the reference file.
- Unsupported details are omitted or explicitly marked as not confirmed by the current documentation context.
- Guidance stays concise and does not import assumptions from Laravel, Composer, package-discovery internals, package source code, or older examples.