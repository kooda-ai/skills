# Configuration And Commands

## Package Identity
- The Laravel AI SDK is documented as `laravel/ai`.
- The docs describe it as the official AI package for Laravel.
- It provides a unified API for multiple AI providers.

## Correct Namespace Imports
Documented correct imports:

```php
use Laravel\Ai\Image;
use Laravel\Ai\Contracts\Agent;
use Laravel\Ai\Promptable;
```

Documented wrong imports:

```php
use Illuminate\Ai\Image;
use Laravel\AI\Agent;
```

## `config/ai.php`
Documented default keys:

```php
'default' => 'openai',
'default_for_images' => 'gemini',
'default_for_audio' => 'openai',
'default_for_transcription' => 'openai',
'default_for_embeddings' => 'openai',
'default_for_reranking' => 'cohere',
```

Documented embedding cache keys:

```php
'caching' => [
    'embeddings' => [
        'cache' => false,
        'store' => env('CACHE_STORE', 'database'),
    ],
],
```

## Documented Provider Entries
OpenAI:

```php
'openai' => [
    'driver' => 'openai',
    'key' => env('OPENAI_API_KEY'),
    'url' => env('OPENAI_URL', 'https://api.openai.com/v1'),
],
```

Anthropic:

```php
'anthropic' => [
    'driver' => 'anthropic',
    'key' => env('ANTHROPIC_API_KEY'),
],
```

Gemini:

```php
'gemini' => [
    'driver' => 'gemini',
    'key' => env('GEMINI_API_KEY'),
],
```

Azure:

```php
'azure' => [
    'driver' => 'azure',
    'key' => env('AZURE_OPENAI_API_KEY'),
    'url' => env('AZURE_OPENAI_URL'),
    'api_version' => env('AZURE_OPENAI_API_VERSION', '2024-10-21'),
    'deployment' => env('AZURE_OPENAI_DEPLOYMENT', 'gpt-4o'),
],
```

Ollama:

```php
'ollama' => [
    'driver' => 'ollama',
    'key' => env('OLLAMA_API_KEY', ''),
    'url' => env('OLLAMA_BASE_URL', 'http://localhost:11434'),
],
```

Cohere:

```php
'cohere' => [
    'driver' => 'cohere',
    'key' => env('COHERE_API_KEY'),
],
```

## Provider And Model Selection
Documented inline provider/model selection:

```php
use function Laravel\Ai\agent;

$response = agent('You are a helpful assistant.')
    ->prompt(
        prompt: 'Explain machine learning',
        provider: 'anthropic',
        model: 'claude-sonnet-4-20250514'
    );
```

Documented provider failover array:

```php
$response = agent('You are a helpful assistant.')
    ->prompt(
        prompt: 'Explain machine learning',
        provider: [
            'openai' => 'gpt-4o',
            'anthropic' => 'claude-sonnet-4-20250514',
            'gemini' => 'gemini-2.0-flash',
        ]
    );
```

Documented class attributes:

```php
use Laravel\Ai\Attributes\Provider;
use Laravel\Ai\Attributes\Model;
use Laravel\Ai\Attributes\UseSmartestModel;
use Laravel\Ai\Attributes\UseCheapestModel;
```

Examples documented by Context7:

```php
#[Provider('anthropic')]
#[Model('claude-sonnet-4-20250514')]
class ClaudeAgent implements Agent, Conversational, HasTools
{
    use Promptable;
}
```

```php
#[UseSmartestModel]
class ComplexReasoningAgent implements Agent, Conversational, HasTools
{
    use Promptable;
}

#[UseCheapestModel]
class SimpleSummaryAgent implements Agent, Conversational, HasTools
{
    use Promptable;
}
```

## Artisan Commands
Documented commands:

```bash
php artisan make:agent CustomerSupportAgent
php artisan make:agent SentimentAnalyzer --structured
php artisan make:tool WeatherLookupTool
php artisan make:agent-middleware LoggingMiddleware
php artisan ai:chat
php artisan ai:chat --provider=anthropic --model=claude-sonnet-4-20250514
```

Do not add install, publish, migrate, config-cache, queue, or storage commands unless a fresh Context7 lookup confirms them.