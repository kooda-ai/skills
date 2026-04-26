# Agents, Tools, Structured Output, Middleware, And Streaming

## Custom Agent Pattern
Documented imports and contracts:

```php
use Laravel\Ai\Contracts\Agent;
use Laravel\Ai\Contracts\Conversational;
use Laravel\Ai\Contracts\HasTools;
use Laravel\Ai\Contracts\Tool;
use Laravel\Ai\Messages\Message;
use Laravel\Ai\Promptable;
use Stringable;
```

Documented agent methods:

```php
public function instructions(): Stringable|string
public function messages(): iterable
public function tools(): iterable
```

Documented prompt usage:

```php
$response = CustomerSupportAgent::make()->prompt('Where is my order #12345?');
echo $response->text;
```

Also documented:

```php
$response = (new SalesCoach)->prompt('Analyze this transcript...');
echo $response->text;
```

## Tool Pattern
Documented imports and contract:

```php
use Illuminate\Contracts\JsonSchema\JsonSchema;
use Laravel\Ai\Contracts\Tool;
use Laravel\Ai\Tools\Request;
use Stringable;
```

Documented tool methods:

```php
public function description(): Stringable|string
public function handle(Request $request): Stringable|string
public function schema(JsonSchema $schema): array
```

Documented request access:

```php
$orderId = $request->get('order_id');
$email = $request->get('email');
```

Documented schema examples:

```php
return [
    'order_id' => $schema->string()->description('The order ID to look up'),
    'email' => $schema->string()->format('email')->description('Customer email address'),
];
```

The docs state that the agent automatically calls the tool when needed.

## Structured Output
Documented imports and contract:

```php
use Illuminate\Contracts\JsonSchema\JsonSchema;
use Laravel\Ai\Contracts\Agent;
use Laravel\Ai\Contracts\HasStructuredOutput;
use Laravel\Ai\Promptable;
```

Documented pattern:

```php
class Reviewer implements Agent, HasStructuredOutput
{
    use Promptable;

    public function instructions(): string { return 'Review and score content.'; }

    public function schema(JsonSchema $schema): array
    {
        return [
            'feedback' => $schema->string()->required(),
            'score' => $schema->integer()->min(1)->max(10)->required(),
        ];
    }
}

$response = (new Reviewer)->prompt('Review this...');
echo $response['score'];
```

The docs show array-style access for structured output responses.

## Agent Middleware
Documented imports and types:

```php
use Closure;
use Laravel\Ai\Prompts\AgentPrompt;
use Laravel\Ai\Responses\AgentResponse;
use Illuminate\Support\Facades\Log;
use Laravel\Ai\Contracts\HasMiddleware;
```

Documented middleware method:

```php
public function handle(AgentPrompt $prompt, Closure $next)
```

Documented response handling:

```php
return $next($prompt)->then(function (AgentResponse $response) use ($prompt) {
    Log::info('Agent response', [
        'agent' => get_class($prompt->agent),
        'tokens' => $response->usage->totalTokens,
    ]);
});
```

Documented agent-side middleware registration:

```php
public function middleware(): array
{
    return [
        LogAgentInteractions::class,
        RateLimitMiddleware::class,
    ];
}
```

Do not invent built-in middleware classes or middleware ordering behavior unless a fresh Context7 lookup confirms them.

## Streaming
Documented streaming example:

```php
return (new SalesCoach)->stream('Analyze this transcript...');
```

The docs describe this as returning an SSE response from a route. Do not add lower-level streaming event APIs unless a fresh Context7 lookup confirms them.