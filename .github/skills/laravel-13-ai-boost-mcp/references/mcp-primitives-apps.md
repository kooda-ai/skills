# Laravel MCP Primitives and App Resources

## Tools
- Create an MCP tool with `php artisan make:mcp-tool CurrentWeatherTool`.
- The documented tool example uses namespace `App\Mcp\Tools`.
- The documented tool example imports `Illuminate\Contracts\JsonSchema\JsonSchema`, `Laravel\Mcp\Request`, `Laravel\Mcp\Response`, `Laravel\Mcp\Server\Attributes\Description`, and `Laravel\Mcp\Server\Tool`.
- The documented tool example extends `Tool`, implements `handle(Request $request): Response`, and defines `schema(JsonSchema $schema): array` for input parameters.
- The documented tool example returns `Response::text(...)`.

## Prompts
- Create an MCP prompt with `php artisan make:mcp-prompt DescribeWeatherPrompt`.
- The documented prompt validation example uses namespace `App\Mcp\Prompts`.
- The documented prompt validation example imports `Laravel\Mcp\Request`, `Laravel\Mcp\Response`, and `Laravel\Mcp\Server\Prompt`.
- The documented prompt validation example extends `Prompt` and validates incoming prompt arguments inside `handle(Request $request): Response` with `$request->validate(...)`.
- The docs emphasize clear error messages for AI clients when prompt validation fails.

## Resources
- Create an MCP resource with `php artisan make:mcp-resource WeatherGuidelinesResource`.
- Resource template examples implement `Laravel\Mcp\Server\Contracts\HasUriTemplate` and return a `Laravel\Mcp\Support\UriTemplate` from `uriTemplate()`.
- Resource template examples use `$request->get(...)` to access extracted URI variables.
- Resource examples return `Response::text(...)`.
- The docs show `#[MimeType('image/png')]` on a `Resource` class for blob MIME type configuration.

## App Resources
- Create an MCP app resource with `php artisan make:mcp-app-resource WeatherDashboardApp`.
- The docs state this command generates an app resource class and a corresponding Blade view.
- The documented app resource example uses namespace `App\Mcp\Resources`, `Laravel\Mcp\Server\AppResource`, `Description`, and `AppMeta`.
- The documented app resource example extends `AppResource` and returns `Response::view('mcp.weather-dashboard-app', ['title' => $this->title()])` from `handle(...)`.

## Metadata
- The docs show result-level metadata by wrapping content with `Response::make(...)` and calling `withMeta(...)` on the response factory.

```php
return Response::make(
    Response::text('The weather is sunny.')
)->withMeta(['request_id' => '12345']);
```

## Boundaries
- Run a fresh Context7 lookup before using output schemas, tool annotations, conditional registration, dependency injection details, prompt arguments, resource annotations, app rendering from tools, app visibility, app CSP/permissions, image/audio responses, streaming responses, or client-side MCP app APIs.
- Do not infer MCP protocol semantics from the framework snippets alone.
