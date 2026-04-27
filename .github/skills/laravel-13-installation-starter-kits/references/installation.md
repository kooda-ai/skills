# Installation

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x installation and application creation.

## Installing The Laravel Installer
The docs show installing the Laravel installer with Composer when PHP and Composer are already present:

```shell
composer global require laravel/installer
```

Run a fresh lookup before stating PHP, Composer, Node, npm, database, operating-system, or PATH requirements.

## Creating An Application
The docs show creating a new Laravel application with the Laravel installer:

```bash
laravel new example-app
```

The starter kits docs also show:

```shell
laravel new my-app
```

The docs state the installer will prompt for framework and starter kit preferences.

## Running The Application Locally
The docs show navigating into the application directory, installing frontend dependencies, building assets, and starting the development server with Composer's `dev` script:

```bash
cd example-app
npm install && npm run build
composer run dev
```

The docs state the application will be accessible at `http://localhost:8000`.

## Laravel Sail Boundary
The docs show installing Sail as a development dependency with Composer:

```shell
composer require laravel/sail --dev
```

Run a fresh lookup before giving Sail setup, Docker, shell alias, service selection, startup, testing, database, or production guidance.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using Laravel Herd, Composer create-project, PHP/Composer/Node version requirements, database prompts, testing framework prompts, starter kit command flags, local development options beyond `composer run dev`, Docker setup, Sail usage beyond installation, or deployment setup.
