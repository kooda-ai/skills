# Laravel MCP Authentication, Authorization, and Testing Boundaries

## OAuth Route Registration Boundary
- The Laravel MCP docs show `Mcp::oauthRoutes()` registering OAuth discovery and client registration routes.
- The docs show applying `auth:api` middleware to a web MCP route.

```php
use App\Mcp\Servers\WeatherExample;
use Laravel\Mcp\Facades\Mcp;

Mcp::oauthRoutes();

Mcp::web('/mcp/weather', WeatherExample::class)
    ->middleware('auth:api');
```

## Sanctum Boundary
- The Laravel MCP docs show protecting an MCP server with Sanctum by applying `auth:sanctum` middleware.
- The docs state MCP clients should provide an `Authorization: Bearer <token>` header for Sanctum authentication.

```php
use App\Mcp\Servers\WeatherExample;
use Laravel\Mcp\Facades\Mcp;

Mcp::web('/mcp/demo', WeatherExample::class)
    ->middleware('auth:sanctum');
```

## Authorization Checks
- The Laravel MCP docs show accessing the authenticated user with `$request->user()` inside MCP tools and resources.
- The documented authorization example checks `$request->user()->can('read-weather')`.
- The documented authorization example returns `Response::error('Permission denied.')` when the user is not authorized.

```php
use Laravel\Mcp\Request;
use Laravel\Mcp\Response;

public function handle(Request $request): Response
{
    if (! $request->user()->can('read-weather')) {
        return Response::error('Permission denied.');
    }

    return Response::text('The weather is sunny.');
}
```

## Testing Boundaries
- The current reference confirms MCP authentication and authorization snippets, but does not confirm MCP Inspector commands or MCP server unit-test assertions.
- Before writing MCP testing guidance, run a fresh Context7 lookup for the exact testing topic and verify every command, helper, and assertion.

## Boundaries
- Do not explain Passport installation, Passport authorization views, OAuth scopes, Sanctum token issuing, custom MCP authentication middleware, or bearer token storage unless a fresh Context7 lookup confirms those details for the requested topic.
- Do not infer general Laravel authentication, authorization, Sanctum, Passport, or testing behavior from MCP snippets alone; use the relevant split skill or package-specific docs.
