# Page Routing And Layouts

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 page component, route, layout, title, slot, route parameter, or route model binding topic.

## Creating Page Components
- Create a page component with `php artisan make:livewire pages::post.create`.
- The documented `pages::post.create` example creates `resources/views/pages/post/⚡create.blade.php`.
- The `pages::` prefix organizes components that are full pages separately from reusable UI components.

## Routing To Page Components
- Register a page component route in `routes/web.php` with `Route::livewire('/posts/create', 'pages::post.create')`.
- Visiting the specified URL renders the component as a complete page using the application's layout.
- The docs describe page components as regular components rendered as full pages with access to custom layouts, page titles, route parameters and model binding, and named slots for layouts.

## Layouts
- Components rendered via routes use an application layout file.
- By default, Livewire looks for `layouts::app` at `resources/views/layouts/app.blade.php`.
- `php artisan livewire:layout` generates `resources/views/layouts/app.blade.php`.
- The layout must include a `{{ $slot }}` placeholder.
- The documented layout includes `{{ $title ?? config('app.name') }}` in the `<title>` tag, `@vite(['resources/css/app.css', 'resources/js/app.js'])`, `@livewireStyles` in the head, and `@livewireScripts` before the closing body.
- Change the default page component layout in `config/livewire.php` with `'component_layout' => 'layouts::dashboard'`.
- Use `#[Layout('layouts::dashboard')]` from `Livewire\Attributes\Layout` above a component class for a component-specific layout.
- Alternatively, return `$this->view()->layout('layouts::dashboard')` from the component `render()` method.

## Page Titles
- The layout file should include a dynamic title such as `{{ $title ?? config('app.name') }}`.
- Use `#[Title('Create post')]` from `Livewire\Attributes\Title` above the component class to set a page title.
- Use `$this->view()->title('Create Post')` from `render()` when the page title needs to be set through the fluent method.

## Named Layout Slots
- If the layout has named slots in addition to `$slot`, set their content in the component Blade view with an `<x-slot>` outside the root element.
- The docs show a layout using `$lang ?? app()->getLocale()` and a component view setting `<x-slot:lang>fr</x-slot>` outside the root element.

## Route Parameters
- Define route parameters with `Route::livewire('/posts/{id}', 'pages::show-post')`.
- Livewire passes the parameter to `mount($id)` when the parameter name matches the route parameter `{id}`.
- The docs show using `mount($id)` to assign a public `Post $post` property after calling `Post::findOrFail($id)`.

## Route Model Binding
- Define a route model parameter with `Route::livewire('/posts/{post}', 'pages::show-post')`.
- Accept the model in `mount(Post $post)` when using Laravel route model binding.
- Livewire knows to use route model binding when the `Post` type-hint is prepended to the `$post` parameter in `mount()`.
- The docs also show omitting `mount()` and declaring `public Post $post`; the property is automatically assigned to the model bound via the route's `{post}` parameter.