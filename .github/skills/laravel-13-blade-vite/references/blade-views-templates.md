# Blade Views And Templates

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x views and Blade templates.

## Standard Blade View File
The docs show a Blade template stored in `resources/views/greeting.blade.php`:

```blade
<!-- View stored in resources/views/greeting.blade.php -->

<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```

## Returning Views
The docs show returning a view from a route and passing data:

```php
Route::get('/', function () {
    return view('greeting', ['name' => 'Finn']);
});
```

The docs also show:

```php
Route::get('/', function () {
    return view('greeting', ['name' => 'James']);
});
```

Confirmed helper: `view(...)`.

## Passing Data To Views
The docs show passing data with an associative array:

```php
return view('greetings', ['name' => 'Victoria']);
```

The docs show passing data with chained `with(...)` calls:

```php
return view('greeting')
    ->with('name', 'Victoria')
    ->with('occupation', 'Astronaut');
```

## Displaying Data
The docs show Blade echo syntax:

```blade
Hello, {{ $name }}.
```

The docs state double curly braces automatically encode HTML entities to prevent XSS attacks. The docs also state any valid PHP expression can be placed within the braces:

```blade
The current UNIX timestamp is {{ time() }}.
```

## Component Data Display Baseline
The docs show component view data displayed with standard Blade echo syntax:

```blade
<div class="alert alert-{{ $type }}">
    {{ $message }}
</div>
```

## Topics Requiring Fresh Lookup
Run a new Context7 query before using raw output syntax, Blade comments, layouts, `@extends`, `@section`, `@yield`, `@parent`, includes, stacks, `@once`, fragments, view composers, sharing data with all views, view namespaces, or returning views from controllers beyond the shown route examples.
