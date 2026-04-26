# InterNACHI Modular Package Reference

Use this reference after a fresh Context7 lookup for the exact InterNACHI Modular topic.

## Package Identity
- Context7 library ID: `/internachi/modular`.
- Package name used in the documented install command: `internachi/modular`.
- Context7 description: a module system for Laravel applications that uses Composer path repositories and Laravel package discovery to organize large projects into separate modules.

## Installation
The documented Composer install command is:

```bash
composer require internachi/modular
```

The docs state Laravel's auto-discovery handles the setup.

## Configuration
The documented configuration publish command is:

```bash
php artisan vendor:publish --tag=modular-config
```

The docs state this publishes the package configuration file to allow customization of the default module namespace and that this is recommended for better organization.

## Module Creation
The documented module creation command is:

```bash
php artisan make:module my-module
```

The docs state this scaffolds a new module with a predefined directory structure including `composer.json`, `src`, `tests`, `routes`, `resources`, and `database` folders.

The docs state it also updates the project's `composer.json` to include the new module.

## Composer Path Repository Example
The docs show this example for registering a module as a path repository in the main project's `composer.json`:

```json
{
    "repositories": [
        {
            "type": "path",
            "url": "./app-modules/my-module"
        }
    ],
    "require": {
        "modules/my-module": "*"
    }
}
```

The docs state this enables Composer's autoloading for the module.

## Helper Commands
The docs list these package helper commands:

```bash
php artisan make:module
php artisan modules:cache
php artisan modules:clear
php artisan modules:sync
php artisan modules:list
```

The docs describe the helper commands as covering scaffolding new modules, caching, clearing cache, syncing configurations, and listing all available modules.

## Laravel Feature Auto-Discovery
The docs state modules automatically integrate with these Laravel features:

- Commands are auto-registered with Artisan.
- Migrations will be run by the Migrator.
- Factories are auto-loaded for `factory()`.
- Policies are auto-discovered for your Models.
- Blade components will be auto-discovered.
- Event listeners will be auto-discovered.

## Laravel Make Commands With Module Support
The docs state the package extends most of Laravel's standard `make:` commands with a `--module` option, allowing components to be scaffolded directly within a specified module. The docs also state this leverages existing Laravel tooling and custom stubs.

Documented commands:

```bash
php artisan make:cast MyModuleCast --module=[module name]
php artisan make:controller MyModuleController --module=[module name]
php artisan make:command MyModuleCommand --module=[module name]
php artisan make:component MyModuleComponent --module=[module name]
php artisan make:channel MyModuleChannel --module=[module name]
php artisan make:event MyModuleEvent --module=[module name]
php artisan make:exception MyModuleException --module=[module name]
php artisan make:factory MyModuleFactory --module=[module name]
php artisan make:job MyModuleJob --module=[module name]
php artisan make:listener MyModuleListener --module=[module name]
php artisan make:mail MyModuleMail --module=[module name]
php artisan make:middleware MyModuleMiddleware --module=[module name]
php artisan make:model MyModule --module=[module name]
php artisan make:notification MyModuleNotification --module=[module name]
php artisan make:observer MyModuleObserver --module=[module name]
php artisan make:policy MyModulePolicy --module=[module name]
php artisan make:provider MyModuleProvider --module=[module name]
php artisan make:request MyModuleRequest --module=[module name]
php artisan make:resource MyModule --module=[module name]
php artisan make:rule MyModuleRule --module=[module name]
php artisan make:seeder MyModuleSeeder --module=[module name]
php artisan make:test MyModuleTest --module=[module name]
```

## Module Generation Placeholders
The docs list these placeholders for filenames and file contents when generating new modules:

```text
StubBasePath
StubModuleNamespace
StubComposerNamespace
StubModuleNameSingular
StubModuleNamePlural
StubModuleName
StubClassNamePrefix
StubComposerName
StubMigrationPrefix
StubFullyQualifiedTestCaseBase
StubTestCaseBase
```

The docs state these placeholders allow dynamic customization of generated module files.