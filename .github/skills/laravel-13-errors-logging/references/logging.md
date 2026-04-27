# Logging

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x logging.

## Log Facade Levels
The docs show writing messages with the `Log` facade:

```php
use Illuminate\Support\Facades\Log;

Log::emergency($message);
Log::alert($message);
Log::critical($message);
Log::error($message);
Log::warning($message);
Log::notice($message);
Log::info($message);
Log::debug($message);
```

Confirmed import: `Illuminate\Support\Facades\Log`.

## Log Levels
The docs state Laravel uses Monolog to power logging services.

The docs state Monolog supports all log levels defined in the RFC 5424 specification.

The docs list the log levels in descending severity: `emergency`, `alert`, `critical`, `error`, `warning`, `notice`, `info`, and `debug`.

The docs state the `level` configuration option on specific channels determines the minimum severity required for a message to be processed by that channel.

## Logging Configuration
The docs state logging configuration is stored in `config/logging.php`.

The docs state this file configures application log channels.

The docs state Laravel uses the `stack` channel by default when logging messages.

The docs state the `stack` channel aggregates multiple log channels into a single channel.

## Specific Channels
The docs show logging to a channel other than the default using `Log::channel(...)`:

```php
use Illuminate\Support\Facades\Log;

Log::channel('slack')->info('Something happened!');
```

Confirmed method: `Log::channel('slack')->info(...)`.

## Available Channel Drivers
The docs list these channel drivers as available in every Laravel application:

- `custom`
- `daily`
- `errorlog`
- `monolog`
- `papertrail`
- `single`
- `slack`
- `stack`
- `syslog`

The docs describe the drivers as follows:

- `custom`: calls a specified factory to create a channel.
- `daily`: a `RotatingFileHandler` based Monolog driver that rotates daily.
- `errorlog`: an `ErrorLogHandler` based Monolog driver.
- `monolog`: a Monolog factory driver that may use any supported Monolog handler.
- `papertrail`: a `SyslogUdpHandler` based Monolog driver.
- `single`: a single file or path based logger channel using `StreamHandler`.
- `slack`: a `SlackWebhookHandler` based Monolog driver.
- `stack`: a wrapper to facilitate creating multi-channel channels.
- `syslog`: a `SyslogHandler` based Monolog driver.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using context arrays, `Log::stack()`, on-demand channels, custom channel factory code, concrete `config/logging.php` arrays, deprecations channels, emergency logger behavior, log retention, cloud logging, Slack configuration, Papertrail configuration, or direct Monolog handler configuration.
