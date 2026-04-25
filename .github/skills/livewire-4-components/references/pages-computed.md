# Pages And Computed Properties

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 page component, layout, route, or computed property topic.

## Routing To Page Components
- Route directly to a component with `Route::livewire('/posts/create', 'pages::post.create')` in `routes/web.php`.
- Page components render as complete pages using the application's layout.
- The docs describe page components as regular components with access to custom layouts, page titles, route parameters, model binding, and named slots for layouts.

## Layouts
- By default, Livewire looks for `layouts::app` at `resources/views/layouts/app.blade.php`.
- `php artisan livewire:layout` generates `resources/views/layouts/app.blade.php`.
- The layout must include a `{{ $slot }}` placeholder.
- The documented layout includes `@livewireStyles` in the head and `@livewireScripts` before the closing body.
- The default layout can be changed in `config/livewire.php` with `component_layout`, such as `'component_layout' => 'layouts::dashboard'`.
- Use `#[Layout('layouts::dashboard')]` from `Livewire\Attributes\Layout` above the component class for a component-specific layout.
- Alternatively, call `->layout('layouts::dashboard')` from the component `render()` method.

## Page Titles And Layout Slots
- The layout should include a dynamic title such as `{{ $title ?? config('app.name') }}`.
- Use `#[Title('Create post')]` from `Livewire\Attributes\Title` above the component class for a static page title.
- Use `->title('Create Post')` from `render()` for a dynamic title.
- Named layout slots are set in the component view with `<x-slot:lang>fr</x-slot>` outside the root element.

## Route Parameters And Model Binding
- `Route::livewire('/posts/{id}', 'pages::show-post')` passes the `{id}` parameter to `mount($id)` when the parameter name matches.
- Route model binding works with `Route::livewire('/posts/{post}', 'pages::show-post')` and `mount(Post $post)`.
- The docs show omitting `mount()` and declaring `public Post $post`; Livewire automatically assigns the model bound via the `{post}` route parameter.

## Computed Properties
- Add `#[Computed]` from `Livewire\Attributes\Computed` above a method to expose it as a computed property.
- Computed properties can be accessed inside other component methods and inside templates.
- In templates, computed properties must be accessed on `$this`, such as `$this->user` or `$this->posts`.
- The docs state that computed properties are not supported on `Livewire\Form` objects.
- Computed properties are memoized for the duration of a single component request only.
- Use `unset($this->posts)` to clear a computed property's memo after the underlying property or database state changes.

## Computed Caching
- For per-component-instance caching across requests, use `#[Computed(persist: true)]`.
- Persisted computed properties are cached for 3600 seconds by default.
- Override the default with `#[Computed(persist: true, seconds: 7200)]`.
- Calling `unset()` on a persisted computed property clears both the in-request memo and the underlying Laravel cached value.
- To cache across all components, use `#[Computed(cache: true)]`.
- Set a custom cache key with `#[Computed(cache: true, key: 'homepage-posts')]`.

## When Docs Recommend Computed Properties
- Use computed properties to avoid querying expensive values until a conditional template branch actually needs them.
- Use computed properties in inline templates when `render()` returns a template string and cannot pass data to a separate view.
- Use computed properties when omitting `render()` and relying on Livewire's conventional render method.
- The computed properties docs mention `#[Session]` as an alternative for simple user-specific values that should persist across page refreshes, do not need to be shareable via URL, and are not computationally expensive to store.