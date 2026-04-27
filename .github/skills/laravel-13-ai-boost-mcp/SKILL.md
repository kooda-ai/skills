---
name: laravel-13-ai-boost-mcp
description: 'Use when: working with Laravel 13 AI-assisted development, Laravel Boost, composer require laravel/boost --dev, boost:install, boost:mcp, Boost MCP server configuration, .ai/guidelines, Laravel MCP, laravel/mcp, routes/ai.php, make:mcp-server, make:mcp-tool, make:mcp-prompt, make:mcp-resource, make:mcp-app-resource, MCP tools, prompts, resources, app resources, metadata, authentication, authorization, testing servers, and Laravel 13 AI/MCP code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 AI, Boost, MCP server, MCP tool, MCP prompt, MCP resource, MCP app, auth, or review task'
---

# Laravel 13 AI, Boost, and MCP

## Purpose
Use this skill to create, review, or explain Laravel 13 AI-assisted development, Laravel Boost setup, and Laravel MCP servers, tools, prompts, resources, app resources, authentication, authorization, and testing using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, editor configuration, or review findings, query Context7 for `/websites/laravel_13_x` with the exact AI, Boost, or MCP topic.
2. Do not add Composer packages, Artisan commands, editor MCP JSON, file paths, route files, namespaces, attributes, facades, class names, method names, response helpers, authentication middleware, authorization behavior, testing commands, or assertions unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a namespace or class name in a malformed way, do not copy it into final code. Run a narrower lookup or omit the exact import while preserving only confirmed methods and behavior.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented package names, commands, JSON keys, attributes, methods, route paths, middleware aliases, view names, and example values.
6. Do not infer behavior from older Laravel versions, MCP protocol docs, package source code, editor docs, blog posts, community examples, or general Laravel memory.

## Reference Map
- Laravel Boost installation, Boost MCP server configuration, VS Code Copilot startup steps, and custom AI guidelines: [boost-setup-guidelines.md](./references/boost-setup-guidelines.md)
- Laravel MCP installation, AI route publishing, server generation, server structure, and local/web registration boundaries: [mcp-installation-servers.md](./references/mcp-installation-servers.md)
- MCP tools, prompts, resources, app resources, metadata, response helpers, and primitive boundaries: [mcp-primitives-apps.md](./references/mcp-primitives-apps.md)
- MCP authentication, authorization checks, Sanctum/OAuth route boundaries, and testing boundaries: [mcp-auth-authorization-testing.md](./references/mcp-auth-authorization-testing.md)

## Workflow
1. Identify the exact surface: Laravel Boost installation, Boost MCP server registration, custom AI guidelines, Laravel MCP package installation, AI routes, MCP server creation, server registration, tool, prompt, resource, app resource, metadata, authentication, authorization, MCP testing, or code review.
2. Query Context7 for that exact Laravel 13 AI, Boost, or MCP topic.
3. Load the relevant reference file from the map above.
4. Use only documented Composer commands, Artisan commands, editor JSON keys, file paths, route files, facades, class names, namespaces, attributes, schema methods, validation APIs, response methods, middleware aliases, and assertions.
5. For MCP details not confirmed in the references, such as web server behavior beyond documented snippets, Passport setup details, MCP Inspector behavior, server unit-test assertions, tool output schemas, annotations, conditional registration, app rendering from tools, app visibility, client SDK APIs, or MCP protocol semantics, rely on the fresh Context7 lookup.
6. For Laravel AI SDK agents, providers, chat, structured output, embeddings, vector stores, or testing fakes, use the `laravel-ai-sdk` skill and query `/laravel/ai` docs instead of inferring from Laravel 13 framework docs.
7. For reviews, flag only documented mismatches: wrong package command, missing `vendor:publish --tag=ai-routes`, unconfirmed route file, wrong server registration facade or method, unconfirmed namespace, missing documented response type, unsupported middleware alias, package-specific behavior inferred from framework docs, or editor configuration not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel Boost is installed with `composer require laravel/boost --dev` and configured with `php artisan boost:install` according to the Laravel 13 docs.
- The docs show manual Boost MCP server registration using command `php` and args `['artisan', 'boost:mcp']` under an MCP server named `laravel-boost`.
- The docs show starting the `laravel-boost` MCP server in VS Code Copilot through `MCP: List Servers` and `Start server`.
- Custom Boost AI guidelines can be added as `.blade.php` or `.md` files under `.ai/guidelines/*`, and the docs state they are included with Boost guidelines when `boost:install` runs.
- Laravel MCP is installed with `composer require laravel/mcp`.
- MCP routes are published with `php artisan vendor:publish --tag=ai-routes`, creating `routes/ai.php` for MCP server definitions.
- `php artisan make:mcp-server WeatherServer` is documented for generating an MCP server class.
- MCP server examples use namespace `App\Mcp\Servers`, extend `Laravel\Mcp\Server`, and may use `Name`, `Version`, and `Instructions` attributes.
- MCP server examples register tools, resources, and prompts through protected `$tools`, `$resources`, and `$prompts` arrays.
- The docs show local MCP server registration with `Mcp::local('weather', WeatherServer::class)`.
- The docs show MCP web route registration in authentication examples with `Mcp::web('/mcp/weather', WeatherExample::class)->middleware('auth:api')`.
- MCP tools can be created with `php artisan make:mcp-tool CurrentWeatherTool`; examples extend `Tool`, implement `handle(Request $request): Response`, and may define `schema(JsonSchema $schema): array`.
- MCP prompts can be created with `php artisan make:mcp-prompt DescribeWeatherPrompt`, and prompt argument validation examples use `$request->validate(...)` inside `handle(...)`.
- MCP resources can be created with `php artisan make:mcp-resource WeatherGuidelinesResource`; resource template examples implement `HasUriTemplate` and return a `UriTemplate`.
- MCP app resources can be created with `php artisan make:mcp-app-resource WeatherDashboardApp`; app resource examples extend `AppResource` and return `Response::view(...)`.
- The docs show `Response::text(...)`, `Response::view(...)`, `Response::error(...)`, and `Response::make(...)->withMeta(...)` in MCP examples.
- The docs show OAuth route registration with `Mcp::oauthRoutes()` and `auth:api` middleware, Sanctum protection with `auth:sanctum`, and authorization checks through `$request->user()->can(...)`.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 AI, Boost, or MCP topic.
- Every package name, command, file path, JSON key, route file, namespace, class, attribute, facade, method, middleware alias, response helper, and testing detail is traceable to the lookup or references.
- Boost-specific guidance is not confused with Laravel MCP server implementation details.
- Laravel MCP framework docs are not used to infer Laravel AI SDK behavior.
- Package-specific behavior for Sanctum, Passport, Reverb, Echo, or editor MCP clients is not inferred when the Laravel 13 docs did not confirm it.
- Unconfirmed AI, Boost, or MCP features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
