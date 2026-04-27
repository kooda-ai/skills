---
name: laravel-13-package-development
description: 'Use when: working with Laravel 13 package development, package discovery, composer.json extra laravel providers aliases dont-discover, package service providers, loadRoutesFrom(), publishesMigrations(), mergeConfigFrom(), publishes(), loadViewsFrom(), package translations, Blade package components, package Artisan commands, vendor:publish tags, public assets, optimizes(), reloads(), and Laravel 13 package code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 package discovery, package service provider, package resources, publishing, commands, or review task'
---

# Laravel 13 Package Development

## Purpose
Use this skill to create, review, or explain Laravel 13 package development code using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, package structure guidance, or review findings, query Context7 for `/websites/laravel_13_x` with the exact package-development topic.
2. Do not add Composer metadata, discovery keys, service provider methods, generated paths, package resource loading methods, publish tags, command registration APIs, optimization hooks, component registration APIs, config behavior, route behavior, migration behavior, translation behavior, view behavior, imports, namespaces, or examples unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or class name in a malformed way, do not copy it into final code. Run a narrower lookup or omit the exact import while preserving only confirmed methods and behavior.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented Composer keys, method names, paths, tags, package namespaces, command names, view namespaces, translation namespaces, and example values.
6. Do not infer behavior from older Laravel versions, Composer docs, package skeletons, Packagist conventions, framework source code, blog posts, community package patterns, or general Laravel memory.

## Reference Map
- Package discovery, `composer.json` `extra.laravel.providers`, aliases, `dont-discover`, service-provider purpose, and malformed namespace boundaries: [discovery-providers.md](./references/discovery-providers.md)
- Package routes, migrations, configuration, `loadRoutesFrom()`, `publishesMigrations()`, `mergeConfigFrom()`, and config publishing: [resources-config-routes-migrations.md](./references/resources-config-routes-migrations.md)
- Package translations, JSON translations, language publishing, views, view publishing, Blade components, component namespaces, and anonymous component boundaries: [views-translations-components.md](./references/views-translations-components.md)
- Package commands, publish groups, public assets, `vendor:publish`, `optimizes()`, and `reloads()`: [commands-publishing-optimization.md](./references/commands-publishing-optimization.md)

## Workflow
1. Identify the exact surface: package discovery, discovery opt-out, package service provider, route loading, migration publishing, config publishing, config merging, translation loading, JSON translation loading, language publishing, view loading, view publishing, Blade component registration, package command registration, public asset publishing, tagged publish groups, optimize hooks, reload hooks, or package code review.
2. Query Context7 for that exact Laravel 13 package-development topic.
3. Load the relevant reference file from the map above.
4. Use only documented Composer keys, service-provider methods, helper paths, package names, tags, commands, facades, methods, and examples.
5. For package topics not in the references, such as package testbench setup, package auto-discovery internals, package config file structure, route middleware groups, migration stub naming, package assets beyond public publishing, package translations beyond documented namespaces, package upgrade paths, package semantic versioning, or package distribution workflow, rely on the fresh Context7 lookup.
6. For reviews, flag only documented mismatches: malformed provider namespace copied from Context7, missing documented discovery entry, unsupported `dont-discover` syntax, using resource loading methods in the wrong provider method, unconfirmed publish tag, unconfirmed package path, `mergeConfigFrom()` nested merge assumptions, package commands registered outside the documented console guard, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Package discovery can be configured in a package's `composer.json` `extra.laravel.providers` array.
- Package discovery can also list facade aliases under `extra.laravel.aliases`.
- Laravel automatically registers package service providers and facades when an installed package is configured for discovery according to the docs.
- Consumers can disable discovery for a package using `extra.laravel.dont-discover` with a package name, or disable discovery for all packages using `*`.
- The docs state a package service provider connects the package to Laravel, binds things into the service container, and tells Laravel where to load package resources such as views, configuration, and language files.
- The package docs state the base service provider class is in the `illuminate/support` Composer package, but the returned namespace text was malformed; run a fresh lookup before writing the exact import.
- `loadRoutesFrom(__DIR__.'/../routes/web.php')` is documented in a package service provider `boot()` method.
- `publishesMigrations([__DIR__.'/../database/migrations' => database_path('migrations')])` is documented for package migrations, and the docs state Laravel updates migration filenames with the current date and time when published.
- `$this->publishes([__DIR__.'/../config/courier.php' => config_path('courier.php')])` is documented for publishing package configuration.
- `mergeConfigFrom(__DIR__.'/../config/courier.php', 'courier')` is documented in `register()`, and the docs state it only merges the first level of the configuration array.
- `loadViewsFrom(__DIR__.'/../resources/views', 'courier')` and `view('courier::dashboard')` are documented for package views.
- `loadTranslationsFrom(__DIR__.'/../lang', 'courier')`, `trans('courier::messages.welcome')`, and `loadJsonTranslationsFrom(__DIR__.'/../lang')` are documented for package translations.
- Package language files can be published to `$this->app->langPath('vendor/courier')`.
- The docs show `Blade::component(...)`, `Blade::componentNamespace(...)`, `Blade::anonymousComponentPath(...)`, and package anonymous components rendered with namespace prefixes such as `<x-courier::alert />`.
- Package Artisan commands can be registered inside `if ($this->app->runningInConsole())` with `$this->commands([...])`.
- Public assets and other publishable file groups can use `$this->publishes(...)` with tags.
- The docs show `php artisan vendor:publish --tag=public --force`, `php artisan vendor:publish --tag=courier-config`, and `php artisan vendor:publish --provider="Your\Package\ServiceProvider"`.
- The docs show `optimizes(optimize: 'package:optimize', clear: 'package:clear-optimizations')` and `reloads('package:reload')` inside a console guard.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 package-development topic.
- Every Composer key, service-provider method, package path, helper, facade, command, tag, namespace, view name, translation key, and behavior statement is traceable to the lookup or references.
- Composer, package distribution, package testing, package skeleton, Packagist, and framework internals are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed package-development features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
