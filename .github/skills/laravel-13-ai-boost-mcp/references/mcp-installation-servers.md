# Laravel MCP Installation and Servers

## Installation and Routes
- Install Laravel MCP with `composer require laravel/mcp`.
- Publish MCP routes with `php artisan vendor:publish --tag=ai-routes`.
- The Laravel MCP docs state the publish command creates `routes/ai.php` for MCP server definitions.

## Server Generation
- Create an MCP server with `php artisan make:mcp-server WeatherServer`.
- The documented server example uses namespace `App\Mcp\Servers`.
- The documented server class extends `Laravel\Mcp\Server`.
- The documented server example uses `Laravel\Mcp\Server\Attributes\Instructions`, `Name`, and `Version` attributes.
- The documented server example registers tools, resources, and prompts with protected `$tools`, `$resources`, and `$prompts` arrays.

```php
use Laravel\Mcp\Server\Attributes\Instructions;
use Laravel\Mcp\Server\Attributes\Name;
use Laravel\Mcp\Server\Attributes\Version;
use Laravel\Mcp\Server;

#[Name('Weather Server')]
#[Version('1.0.0')]
#[Instructions('This server provides weather information and forecasts.')]
class WeatherServer extends Server
{
    protected array $tools = [];

    protected array $resources = [];

    protected array $prompts = [];
}
```

## Server Registration
- The docs show local MCP server registration with `Laravel\Mcp\Facades\Mcp` and `Mcp::local('weather', WeatherServer::class)`.

```php
use App\Mcp\Servers\WeatherServer;
use Laravel\Mcp\Facades\Mcp;

Mcp::local('weather', WeatherServer::class);
```

- The docs show web MCP server registration in authentication examples with `Mcp::web('/mcp/weather', WeatherExample::class)->middleware('auth:api')`.

## Boundaries
- Run a fresh Context7 lookup before describing web server behavior beyond the documented `Mcp::web(...)` snippets.
- Do not use `mcp:start`, server transport behavior, MCP client startup behavior, or server inspection commands unless a fresh Context7 lookup confirms them.
- Do not infer package directory paths beyond the documented namespace and route file unless the current lookup confirms the generated path.
