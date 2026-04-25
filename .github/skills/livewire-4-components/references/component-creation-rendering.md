# Component Creation And Rendering

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 component creation or rendering topic.

## Component Formats
- `php artisan make:livewire post.create` creates a single-file component at `resources/views/components/post/⚡create.blade.php`.
- Page components use the `pages::` namespace, for example `php artisan make:livewire pages::post.create`, which creates `resources/views/pages/post/⚡create.blade.php`.
- `php artisan make:livewire post.create --mfc` creates a multi-file component directory at `resources/views/components/post/⚡create/`.
- Multi-file component files documented by the docs are `create.php`, `create.blade.php`, optional `create.js`, optional `create.css`, optional `create.global.css`, and optional `create.test.php` when `--test` is used.
- `php artisan make:livewire CreatePost --class` creates `app/Livewire/CreatePost.php` and `resources/views/livewire/create-post.blade.php`.

## Command Options
The docs list these `make:livewire` options:

- `--sfc`: create a single-file component; this is the default.
- `--mfc`: create a multi-file component.
- `--class`: create a class-based component.
- `--type=sfc|mfc|class`: set the component type explicitly.
- `--emoji=true|false`: override the config emoji setting for this command.
- `--test`: include a Pest test file.
- `--js`: include a JavaScript file for multi-file components only.
- `--css`: include CSS files for multi-file components only.

## Format Selection
- Single-file components are documented as the default, best for most components, easy to understand at a glance, and suited to small or medium components.
- Multi-file components are documented as better for large or complex components, improved IDE support and navigation, and clearer separation when components have significant JavaScript.
- Class-based components are documented for teams migrating from Livewire v2 or v3, teams that prefer a traditional file structure, or teams with established class-based conventions.
- For a new Livewire 4 project, the docs point to single-file or multi-file components for the latest Livewire conventions.

## Converting Formats
- `php artisan livewire:convert post.create` auto-detects and converts.
- `php artisan livewire:convert post.create --mfc` explicitly converts to multi-file.
- `php artisan livewire:convert post.create --sfc` explicitly converts to single-file.
- The docs warn that test files are deleted when converting multi-file components to single-file format, and the command prompts for confirmation because test files cannot be preserved in the single-file format.

## Rendering Components
- Render a component in Blade with `<livewire:component-name />`.
- Use dot notation for components in subdirectories, such as `<livewire:post.create />` for `resources/views/components/post/⚡create.blade.php`.
- Use namespace prefixes for namespaced components, such as `<livewire:pages::post.create />`.
- The docs state that the component name used in Blade tags and routes is the same across single-file, multi-file, and class-based formats.

## File Path Mapping
The docs map these formats to the same component names:

- `resources/views/components/post/⚡create.blade.php` -> `post.create`.
- `resources/views/components/post/⚡create/create.php` -> `post.create`.
- `app/Livewire/Post/Create.php` -> `post.create`.
- `resources/views/pages/post/⚡create.blade.php` -> `pages::post.create`.
- `resources/views/pages/post/⚡create/create.php` -> `pages::post.create`.

## Passing Props
- Pass static props with attributes: `<livewire:post.create title="Initial Title" />`.
- Pass dynamic values with a colon: `<livewire:post.create :title="$initialTitle" />`.
- Receive passed data in `mount($title = null)`; the docs describe `mount()` as similar to a constructor and running when the component initializes, not on subsequent requests within a page session.
- To reduce boilerplate, omit `mount()` when public property names match passed values; Livewire automatically sets matching properties.
- The docs warn that passed properties are not reactive by default when the outer value changes after initial page load.

## Route Parameters As Props
- Page components can receive route parameters directly through `mount()`.
- `Route::livewire('/posts/{id}', 'pages::post.show')` passes `{id}` to `mount($id)`.
- Livewire supports route model binding with `Route::livewire('/posts/{post}', 'pages::post.show')` and `mount(Post $post)`.
- The docs also show that a public `Post $post` property can be automatically assigned from the route model binding when the property matches the route parameter and no `mount()` method is needed.

## Accessing Data In Views
- Public properties are automatically available in the Blade template, such as `{{ $title }}`.
- The docs state that protected properties must be accessed with `$this->`, are never sent to the frontend, cannot be manipulated by users, and are not persisted between requests.
- Computed properties are accessed in templates through `$this`, such as `$this->posts`.
- A `render()` method can pass data with `$this->view([...])`; the docs warn that `render()` runs on every component update, so expensive operations should be avoided there unless fresh data is needed every update.

## Organizing Components
- By default, `pages::` points to `resources/views/pages/` and `layouts::` points to `resources/views/layouts/`.
- Additional component namespaces can be configured in `config/livewire.php` under `component_namespaces`.
- Additional component discovery directories can be configured in `config/livewire.php` under `component_locations`.
- Programmatic registration in a service provider is documented with `Livewire::addComponent(name: ..., viewPath: ...)`, `Livewire::addLocation(viewPath: ...)`, and `Livewire::addNamespace(namespace: ..., viewPath: ...)`.
- For class-based components, the docs show `Livewire::addComponent(name: ..., class: ...)`, `Livewire::addLocation(classNamespace: ...)`, and `Livewire::addNamespace(namespace: ..., classNamespace: ..., classPath: ..., classViewPath: ...)`.

## Stubs And Defaults
- `php artisan livewire:stubs` publishes customizable component stubs.
- Documented stubs include `stubs/livewire-sfc.stub`, `stubs/livewire-mfc-class.stub`, `stubs/livewire-mfc-view.stub`, `stubs/livewire-mfc-js.stub`, `stubs/livewire-mfc-test.stub`, `stubs/livewire.stub`, `stubs/livewire.view.stub`, `stubs/livewire.attribute.stub`, and `stubs/livewire.form.stub`.
- The docs show `config/livewire.php` `make_command` settings for disabling the emoji and restoring v3-style class-based defaults with `'type' => 'class'` and `'emoji' => false`.

## Troubleshooting
- For "component not found" errors, the docs say to verify the component file path, component name, namespace configuration, and optionally clear the view cache with `php artisan view:clear`.
- For blank or non-rendering components, documented common causes include a missing root element, syntax errors in the PHP section, and Laravel log errors.
- Livewire requires exactly one root element in a Blade template.
- For class-name conflicts in single-file components, the docs say to rename one component or namespace one directory.