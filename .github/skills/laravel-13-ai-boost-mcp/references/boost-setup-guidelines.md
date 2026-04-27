# Laravel Boost Setup and AI Guidelines

## Confirmed Boost Setup
- Install Laravel Boost as a development dependency with `composer require laravel/boost --dev`.
- Run the interactive installer with `php artisan boost:install`.
- The Laravel 13 installation docs state Boost installation uses Composer and then an interactive Artisan command that configures IDE and AI agent integrations.

## Boost MCP Server
- The Laravel Boost docs show a manual MCP server configuration named `laravel-boost`.
- The documented command is `php`.
- The documented args are `['artisan', 'boost:mcp']`.

```json
{
    "mcpServers": {
        "laravel-boost": {
            "command": "php",
            "args": ["artisan", "boost:mcp"]
        }
    }
}
```

## VS Code Copilot Startup
The Laravel Boost docs confirm this VS Code Copilot startup flow:

1. Open the command palette with `Cmd+Shift+P` or `Ctrl+Shift+P`.
2. Select `MCP: List Servers`.
3. Select `laravel-boost`.
4. Choose `Start server`.

## Custom AI Guidelines
- The Laravel 13 docs confirm custom AI guidelines can be added to `.ai/guidelines/*`.
- Guideline files may be `.blade.php` or `.md` files.
- The docs state these files are automatically included with Laravel Boost's guidelines when `boost:install` runs.

## Boundaries
- Do not invent Boost tool names, Boost MCP capabilities, installed editor file paths, or IDE-specific configuration files unless the fresh Context7 lookup confirms them.
- Do not describe Laravel MCP server implementation from Boost docs alone; use the MCP references and a fresh MCP lookup.
- Do not infer Laravel AI SDK behavior from Boost documentation; use the `laravel-ai-sdk` skill and `/laravel/ai` docs for SDK-specific work.
