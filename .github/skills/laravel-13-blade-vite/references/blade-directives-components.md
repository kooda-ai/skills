# Blade Directives And Components

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Blade directives and component props.

## Conditional Directives
The docs describe Blade directives as shortcuts for common PHP control structures. The returned docs explicitly mention conditional directives such as `@if`, `@elseif`, `@else`, and `@endif`, plus specialized directives `@unless`, `@isset`, and `@empty`.

Run a narrower lookup before using exact conditional examples beyond those directive names.

## Loop Directives
The docs show loop directives:

```blade
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor

@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach

@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse

@while (true)
    <p>I'm looping forever.</p>
@endwhile
```

Confirmed loop directives: `@for`, `@endfor`, `@foreach`, `@endforeach`, `@forelse`, `@empty`, `@endforelse`, `@while`, and `@endwhile`.

## Switch Directives
The docs show switch directives:

```blade
@switch($i)
    @case(1)
        First case...
        @break

    @case(2)
        Second case...
        @break

    @default
        Default case...
@endswitch
```

Confirmed switch directives: `@switch`, `@case`, `@break`, `@default`, and `@endswitch`.

## Form Element State Directives
The docs show directives that conditionally render form element attributes based on boolean expressions.

`@checked` example:

```blade
<input
    type="checkbox"
    name="active"
    value="active"
    @checked(old('active', $user->active))
/>
```

`@selected` example:

```blade
<select name="version">
    @foreach ($product->versions as $version)
        <option value="{{ $version }}" @selected(old('version') == $version)>
            {{ $version }}
        </option>
    @endforeach
</select>
```

Other documented examples:

```blade
<button type="submit" @disabled($errors->isNotEmpty())>Submit</button>
```

```blade
<input
    type="email"
    name="email"
    value="email@laravel.com"
    @readonly($user->isNotAdmin())
/>
```

```blade
<input
    type="text"
    name="title"
    value="title"
    @required($user->isAdmin())
/>
```

Confirmed form state directives: `@checked`, `@selected`, `@disabled`, `@readonly`, and `@required`.

## Component Props And Attributes
The docs show a component view using `@props(...)` and the attribute bag:

```blade
<!-- /resources/views/components/alert.blade.php -->

@props(['type' => 'info', 'message'])

<div {{ $attributes->merge(['class' => 'alert alert-'.$type]) }}>
    {{ $message }}
</div>
```

The docs show invoking the component:

```blade
<x-alert type="error" :message="$message" class="mb-4"/>
```

Confirmed component details: `/resources/views/components/alert.blade.php`, `@props(...)`, `$attributes->merge(...)`, `<x-alert ... />`, static attributes, and bound attributes such as `:message="$message"`.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using `@auth`, `@guest`, `@env`, `@production`, `@include`, `@includeIf`, `@each`, `@extends`, `@section`, `@yield`, `@push`, `@stack`, `@once`, `@csrf`, `@method`, class-based components, `php artisan make:component`, anonymous component discovery, slots, inline components, dynamic components, component methods, or custom directives.
