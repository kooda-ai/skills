# Facade Class Reference

Sources used: Current Laravel 13.x documentation page for facades.

## Reference Table Shape
The docs include a facade class reference table with three documented pieces of information:
- facade name
- underlying class
- service-container binding key, where applicable

Use the table as a lookup tool when you need the documented root class or binding key for a facade name.

## Representative Documented Mappings
The docs list the following mappings in the Laravel 13 facade reference table:

| Facade | Underlying Class | Binding Key |
| --- | --- | --- |
| App | `Illuminate\Foundation\Application` | `app` |
| Artisan | `Illuminate\Contracts\Console\Kernel` | `artisan` |
| Cache | `Illuminate\Cache\CacheManager` | `cache` |
| Config | `Illuminate\Config\Repository` | `config` |
| DB | `Illuminate\Database\DatabaseManager` | `db` |
| Event | `Illuminate\Events\Dispatcher` | `events` |
| Gate | `Illuminate\Contracts\Auth\Access\Gate` | none shown |
| Http | `Illuminate\Http\Client\Factory` | none shown |
| Log | `Illuminate\Log\LogManager` | `log` |
| Mail | `Illuminate\Mail\Mailer` | `mailer` |
| Notification | `Illuminate\Notifications\ChannelManager` | none shown |
| Queue | `Illuminate\Queue\QueueManager` | `queue` |
| RateLimiter | `Illuminate\Cache\RateLimiter` | none shown |
| Redirect | `Illuminate\Routing\Redirector` | `redirect` |
| Redis | `Illuminate\Redis\RedisManager` | `redis` |
| Request | `Illuminate\Http\Request` | `request` |
| Response | `Illuminate\Contracts\Routing\ResponseFactory` | none shown |
| Route | `Illuminate\Routing\Router` | `router` |
| Schema | `Illuminate\Database\Schema\Builder` | none shown |
| Session | `Illuminate\Session\SessionManager` | `session` |
| Storage | `Illuminate\Filesystem\FilesystemManager` | `filesystem` |
| URL | `Illuminate\Routing\UrlGenerator` | `url` |
| Validator | `Illuminate\Validation\Factory` | `validator` |
| View | `Illuminate\View\Factory` | `view` |
| Vite | `Illuminate\Foundation\Vite` | none shown |

The docs also list corresponding instance-oriented entries for several facades, such as `Auth (Instance)`, `Cache (Instance)`, `DB (Instance)`, `Password (Instance)`, `Queue (Instance)`, `Redis (Instance)`, `Response (Instance)`, `Session (Instance)`, `Storage (Instance)`, `Validator (Instance)`, and `View (Instance)`.

## Usage Boundary
Use the class reference table to verify the documented root class or binding key for a facade name. Use the owning split skill when the task is about the feature API itself instead of the facade mapping.

## Topics Requiring Fresh Lookup
Run a new documentation lookup before relying on mappings not captured here, custom facades, alias registration behavior, or package-specific facades.