# Redis Commands, Pipelines, Transactions, And Lua

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Redis commands, pipelining, transactions, and Lua scripts.

## Redis Facade Commands
The docs show importing and using the Redis facade:

```php
use Illuminate\Support\Facades\Redis;

Redis::set('name', 'Taylor');

$values = Redis::lrange('names', 5, 10);
```

The docs state dynamic method calls are supported for Redis commands.

## Command Method
The docs show executing a command by name with an array of arguments:

```php
$values = Redis::command('lrange', ['name', 5, 10]);
```

Confirmed method: `Redis::command(...)`.

Run a fresh lookup before adding concrete return types or command-specific behavior.

## Pipelines
The docs state `pipeline(...)` reduces network latency by sending multiple commands to the Redis server in a single batch.

The returned docs show a pipeline closure that loops from `0` to `999` and calls `set` on the pipe for keys like `key:$i`.

Confirmed method: `Redis::pipeline(...)`.

The returned Context7 snippet for pipelining had malformed namespace/import formatting. Run a fresh lookup before writing exact imports or closure parameter types for pipeline examples.

## Transactions
The docs state `transaction(...)` wraps multiple commands into a single atomic operation using a closure.

The returned docs show a transaction closure incrementing `user_visits` and `total_visits`.

Confirmed method: `Redis::transaction(...)`.

The docs state retrieving values within the transaction closure is not supported.

The returned Context7 snippet for transactions had malformed namespace/import formatting. Run a fresh lookup before writing exact imports or closure parameter types for transaction examples.

## Lua Scripts
The docs show executing a Lua script with `Redis::eval(...)`:

```php
$value = Redis::eval(<<<'LUA'
    local counter = redis.call("incr", KEYS[1])

    if counter > 5 then
        redis.call("incr", KEYS[2])
    end

    return counter
LUA, 2, 'first-counter', 'second-counter');
```

The docs describe `eval(...)` as executing Lua scripts on the Redis server, allowing conditional logic and interaction with key values during an atomic operation.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using Redis command return types, command aliases, command-specific PHP argument forms, pipeline return values, transaction return values, watch/unwatch behavior, Lua script key and argument conventions beyond the returned example, Redis locks, or Redis testing helpers.
