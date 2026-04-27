# Server Configuration

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x deployment server configuration, production debug mode, and permissions.

## Debug Mode
The deployment docs state the `APP_DEBUG` environment variable controls how much error information is displayed to users.

In production environments, the docs state this value should always be `false` to prevent exposure of sensitive configuration details.

The configuration docs show `config/app.php` reading the environment value:

```php
'debug' => (bool) env('APP_DEBUG', false),
```

## Web Directory Safety
The docs state Laravel applications should always be served from the root of the web server's configured web directory.

The docs state serving the application from a subdirectory within the web directory is not recommended because it could expose sensitive application files.

## Nginx Public Root Example
The deployment docs show this Nginx example:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name example.com;
    root /srv/example.com/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ ^/index\.php(/|$) {
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
        fastcgi_hide_header X-Powered-By;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

The docs state the `fastcgi_pass` path should match the specific PHP-FPM socket location.

Run a fresh lookup before writing Apache configuration or changing the Nginx example.

## Directory Permissions
The deployment docs state the web server process must have write permissions for the `bootstrap/cache` and `storage` directories.

The docs state these directories are used by the framework to store cached files and application data.

## Public Disk Link Boundary
The filesystem docs show creating the public disk symbolic link:

```shell
php artisan storage:link
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before giving PHP extension requirements, Composer install flags, Node build steps, file ownership commands, chmod/chown commands, Apache examples, TLS configuration, reverse proxy settings, trusted proxy settings, database migration deployment steps, Octane, Forge, Vapor, Envoyer, or Laravel Cloud guidance.
