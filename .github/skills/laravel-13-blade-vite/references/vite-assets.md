# Vite Assets

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Vite integration and frontend asset bundling.

## Default Vite Integration
The docs state Laravel uses Vite by default to bundle CSS and JavaScript assets. The docs describe Vite as offering fast build times and near-instantaneous Hot Module Replacement during development.

The docs state every new Laravel application includes a `vite.config.js` file configured with the Laravel Vite plugin. The docs describe Vite as the standard tool for creating production-ready assets whether using Blade and Livewire or Inertia with a modern JavaScript framework.

## Loading Scripts And Styles
The docs show using `@vite` in the application's root template to load compiled assets:

```blade
<!DOCTYPE html>
<head>
    {{-- ... --}}

    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
```

The docs state this automatically injects the Vite client for HMR in development and loads versioned assets in production.

## JavaScript-Only Entry Point
The docs say if CSS is imported via JavaScript, only include the JavaScript entry point in the `@vite` directive:

```blade
<!DOCTYPE html>
<head>
    {{-- ... --}}

    @vite('resources/js/app.js')
</head>
```

## Production Build
The docs confirm this production build command:

```shell
npm run build
```

The docs describe it as a command to version and bundle application assets for production deployment.

## Vite Configuration Options
The docs show `vite.config.js` using `defineConfig`, `laravel-vite-plugin`, and Laravel plugin options:

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            hotFile: 'storage/vite.hot', // Customize the "hot" file...
            buildDirectory: 'bundle', // Customize the build directory...
            input: ['resources/js/app.js'], // Specify the entry points...
        }),
    ],
    build: {
      manifest: 'assets.json', // Customize the manifest filename...
    },
});
```

Confirmed package/config details: `vite`, `laravel-vite-plugin`, `defineConfig`, `laravel(...)`, `hotFile`, `buildDirectory`, `input`, `build.manifest`, `storage/vite.hot`, `bundle`, `resources/js/app.js`, and `assets.json`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `npm install`, `npm run dev`, React or Vue plugin setup, TypeScript setup, asset aliases, static asset URL handling, environment variables, SSR, CSP nonces, subresource integrity, custom refresh behavior, testing with Vite, or advanced deployment/build options beyond those shown here.
