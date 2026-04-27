---
name: laravel-13-redis
description: 'Use when: working with Laravel 13 Redis, PhpRedis, REDIS_CLIENT, config/database.php redis configuration, REDIS_URL, REDIS_HOST, REDIS_USERNAME, REDIS_PASSWORD, REDIS_PORT, REDIS_DB, REDIS_CACHE_DB, REDIS_CLUSTER, REDIS_PREFIX, Redis facade, Redis::connection(), Redis::set(), Redis::lrange(), Redis::command(), pipeline(), transaction(), eval(), publish(), subscribe(), psubscribe(), and Laravel 13 Redis code reviews. Requires Context7 /websites/laravel_13_x docs before adding details.'
argument-hint: 'Laravel 13 Redis configuration, facade command, pipeline, transaction, pub/sub, or review task'
---

# Laravel 13 Redis

## Purpose
Use this skill to create, review, or explain Laravel 13 Redis configuration and Redis facade usage using only details confirmed in the current Laravel 13.x documentation from Context7.

## Source Rule
1. Before giving final code, commands, setup steps, or review findings, query Context7 for `/websites/laravel_13_x` with the exact Redis topic.
2. Do not add Redis clients, installation steps, configuration keys, environment variables, connection options, facade methods, command behavior, pipeline behavior, transaction behavior, Lua behavior, pub/sub behavior, imports, namespaces, or examples unless they appear in the current Context7 result or the reference files below.
3. If a Context7 result renders a Redis import or facade namespace in a malformed way, do not copy it into final code. Run a narrower lookup or omit the import while preserving only confirmed methods and behavior.
4. If a requested detail is not confirmed by the current Context7 result, run a narrower lookup or explicitly say the current Laravel 13 documentation context does not confirm it.
5. Keep examples close to documented snippets and preserve documented facade names, methods, config keys, environment variables, channel names, command names, and example values.
6. Do not infer behavior from older Laravel versions, Redis server docs, PhpRedis docs, Predis docs, queue/cache/session docs, package docs, source code, blog posts, or general Laravel memory.

## Reference Map
- Redis client selection, `config/database.php`, `REDIS_CLIENT`, default/cache connections, connection options, prefixes, and named connections: [configuration-connections.md](./references/configuration-connections.md)
- Redis facade command execution, dynamic command methods, `Redis::command(...)`, pipelining, transactions, Lua `eval(...)`, and malformed import boundaries: [commands-pipelines-transactions.md](./references/commands-pipelines-transactions.md)
- Redis pub/sub, `publish(...)`, `subscribe(...)`, long-running Artisan command subscribers, and wildcard `psubscribe(...)`: [pub-sub.md](./references/pub-sub.md)

## Workflow
1. Identify the exact surface: Redis client configuration, default connection, cache connection, named connection, Redis facade command, direct command method, `Redis::command(...)`, pipeline, transaction, Lua script, publishing, subscribing, wildcard subscribing, or Redis code review.
2. Query Context7 for that exact Laravel 13 Redis topic.
3. Load the relevant reference file from the map above.
4. Use only documented config keys, environment variables, facade methods, connection names, command examples, channel names, closure shapes, and behavior statements.
5. For Redis topics not in the references, such as Predis installation, PhpRedis extension installation, Redis Sentinel, TLS, persistent connections, cluster configuration details beyond the returned `REDIS_CLUSTER` option, connection aliases, serializer/compression options, cache/session/queue Redis usage, testing Redis code, or Redis server operations, rely on the fresh Context7 lookup.
6. For reviews, flag only documented mismatches: unconfirmed client, unconfirmed config key, wrong connection name assumption, malformed imports copied from Context7, unsupported facade method, retrieving values inside a transaction closure, unconfirmed pub/sub behavior, or behavior not confirmed by the current lookup.

## Confirmed Core Patterns
- Laravel Redis configuration lives in `config/database.php` according to the returned Redis docs.
- The Redis client is configured under `redis.client` with `env('REDIS_CLIENT', 'phpredis')`.
- The docs state PhpRedis is the default client for Laravel.
- The docs show Redis options including `cluster` from `REDIS_CLUSTER` and `prefix` from `REDIS_PREFIX` with an `APP_NAME`-based default.
- The docs show a `default` Redis connection using `REDIS_URL`, `REDIS_HOST`, `REDIS_USERNAME`, `REDIS_PASSWORD`, `REDIS_PORT`, and `REDIS_DB`.
- The docs show a `cache` Redis connection using `REDIS_URL`, `REDIS_HOST`, `REDIS_USERNAME`, `REDIS_PASSWORD`, `REDIS_PORT`, and `REDIS_CACHE_DB`.
- The docs show obtaining a named connection with `Redis::connection('connection-name')` and the default connection with `Redis::connection()`.
- The docs show `Redis::set('name', 'Taylor')` and `Redis::lrange('names', 5, 10)` as direct Redis facade command calls.
- The docs state dynamic method calls are supported for Redis commands.
- The docs show `Redis::command('lrange', ['name', 5, 10])` as an alternate command execution pattern.
- The docs show `Redis::pipeline(...)` for reducing network latency by sending multiple commands in one batch.
- The docs show `Redis::transaction(...)` for wrapping multiple commands in an atomic operation and state retrieving values within the transaction closure is not supported.
- The docs show `Redis::eval(...)` for executing Lua scripts on the Redis server.
- The docs show `Redis::publish('test-channel', json_encode([...]))` for publishing messages.
- The docs show `Redis::subscribe(['test-channel'], function (string $message) { ... })` inside an Artisan command because subscribing begins a long-running process.
- The docs show `Redis::psubscribe(['*'], function (string $message, string $channel) { ... })` and `Redis::psubscribe(['users.*'], function (string $message, string $channel) { ... })` for wildcard subscriptions.

## Completion Check
- A fresh Context7 lookup was performed for the exact Laravel 13 Redis topic.
- Every config key, environment variable, facade method, connection name, command, import, channel name, closure parameter, and behavior statement is traceable to the lookup or references.
- Redis server, Predis, PhpRedis extension, cache/session/queue, clustering, Sentinel, and operational details are not inferred when the Laravel 13 docs did not confirm them.
- Unconfirmed Redis features are omitted or explicitly marked as not confirmed by the current Laravel 13 documentation context.
