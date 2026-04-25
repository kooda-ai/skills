# Module Foundation

Use this reference after a fresh Context7 lookup for the exact Filament 5 Advanced Modular Architecture topic.

## Modular Approach
- The docs describe modular architecture as a way to organize large-scale Filament applications by splitting them into self-contained modules based on Domain-Driven Design principles.
- The docs state each module acts as a distinct domain.
- The docs state each module is structured as a separate Composer package, typically housed within an `app-modules` directory.
- Do not add DDD tactics beyond this documented scope unless a fresh Context7 result confirms them.

## Documented Module Directory Example

```text
.
+-- app-modules
|   +-- alerts
|   |   +-- composer.json
|   |   +-- config
|   |   |   +-- alerts.php
|   |   +-- database
|   |   |   +-- factories
|   |   |   +-- migrations
|   |   |   +-- seeders
|   |   +-- resources
|   |   |   +-- views
|   |   |   |   +-- filament
|   |   |   |   |   +-- pages
|   |   +-- routes
|   |   |   +-- web.php
|   |   +-- src
|   |   |   +-- AlertsPlugin.php
|   |   |   +-- Filament
|   |   |   |   +-- Pages
|   |   |   |   +-- Resources
|   |   |   |   |   +-- Alerts
|   |   |   |   |   |   +-- AlertResource.php
|   |   |   |   |   |   +-- Pages
|   |   |   |   |   |   |   +-- CreateAlert.php
|   |   |   |   |   |   |   +-- EditAlert.php
|   |   |   |   |   |   |   +-- ListAlerts.php
|   |   |   |   +-- Widgets
|   |   |   +-- Models
|   |   |   |   +-- Alert.php
|   |   |   +-- Providers
|   |   |   |   +-- AlertsServiceProvider.php
|   |   +-- tests
```

## Documented Module Composer Metadata

```json
{
    "name": "my-app/alerts",
    "type": "library",
    "require": {
        "filament/filament": "^5.0"
    },
    "autoload": {
        "psr-4": {
            "Modules\\Alerts\\": "src/"
        }
    },
    "extra": {
        "laravel": {
            "providers": [
                "Modules\\Alerts\\Providers\\AlertsServiceProvider"
            ]
        }
    }
}
```

## Use Boundaries
- Use the documented `app-modules/alerts` example as an example, not a universal requirement.
- Do not introduce module generator commands, package installers, domain service layers, repositories, aggregates, or value objects unless the active Context7 lookup confirms them.