# Redis Configuration And Connections

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Redis configuration and connections.

## Client Selection
The docs show Redis client selection in the `redis` configuration array:

```php
'redis' => [

    'client' => env('REDIS_CLIENT', 'phpredis'),

    // ...
],
```

The docs state PhpRedis is Laravel's default Redis client.

Run a fresh lookup before adding Predis installation, PhpRedis extension installation, client aliases, serializer options, compression options, persistent connection options, or client-specific behavior.

## Redis Server Configuration
The docs show Redis server configuration in the application's `config/database.php` configuration file:

```php
'redis' => [

    'client' => env('REDIS_CLIENT', 'phpredis'),

    'options' => [
        'cluster' => env('REDIS_CLUSTER', 'redis'),
        'prefix' => env('REDIS_PREFIX', Str::slug(env('APP_NAME', 'laravel'), '_').'_database_'),
    ],

    'default' => [
        'url' => env('REDIS_URL'),
        'host' => env('REDIS_HOST', '127.0.0.1'),
        'username' => env('REDIS_USERNAME'),
        'password' => env('REDIS_PASSWORD'),
        'port' => env('REDIS_PORT', '6379'),
        'database' => env('REDIS_DB', '0'),
    ],

    'cache' => [
        'url' => env('REDIS_URL'),
        'host' => env('REDIS_HOST', '127.0.0.1'),
        'username' => env('REDIS_USERNAME'),
        'password' => env('REDIS_PASSWORD'),
        'port' => env('REDIS_PORT', '6379'),
        'database' => env('REDIS_CACHE_DB', '1'),
    ],

]
```

Confirmed environment variables from this snippet: `REDIS_CLIENT`, `REDIS_CLUSTER`, `REDIS_PREFIX`, `APP_NAME`, `REDIS_URL`, `REDIS_HOST`, `REDIS_USERNAME`, `REDIS_PASSWORD`, `REDIS_PORT`, `REDIS_DB`, and `REDIS_CACHE_DB`.

Confirmed connection names from this snippet: `default` and `cache`.

Run a fresh lookup before changing defaults, adding extra options, describing cluster behavior, or adding imports for `Str` in configuration files.

## Multiple Redis Connections
The docs state `config/database.php` allows multiple Redis connections and servers to be defined.

The docs show obtaining a named or default Redis connection:

```php
$redis = Redis::connection('connection-name');
$redis = Redis::connection();
```

Confirmed method: `Redis::connection(...)`.

Run a fresh lookup before adding concrete custom connection arrays, connection pooling behavior, connection error handling, or connection-specific client behavior.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using Redis Sentinel, TLS, Unix sockets, persistent connections, cluster node arrays, Predis setup, PhpRedis installation, serializer/compression options, Redis aliases, cache/session/queue Redis configuration, broadcasting Redis configuration, or Redis server administration commands.
