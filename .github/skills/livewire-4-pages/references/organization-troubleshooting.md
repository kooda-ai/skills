# Organization And Troubleshooting

Use this reference only after a fresh Context7 lookup confirms the relevant Livewire 4 page component organization, namespace, registration, generation, rendering, or troubleshooting topic.

## Page Component Formats And Names
- `php artisan make:livewire pages::post.create` creates a single-file page component at `resources/views/pages/post/⚡create.blade.php`.
- The docs map `resources/views/pages/post/⚡create.blade.php` to `pages::post.create`.
- The docs map `resources/views/pages/post/⚡create/create.php` to `pages::post.create` for a multi-file namespaced component.
- The component name used in Blade tags and routes is the same across single-file, multi-file, and class-based formats.
- Render a namespaced component in Blade with `<livewire:pages::post.create />`.
- Use dot notation for subdirectories and a namespace prefix for namespaced components.

## Component Generation Options
- `--sfc` creates a single-file component and is the default.
- `--mfc` creates a multi-file component.
- `--class` creates a class-based component.
- `--type=sfc|mfc|class` sets the component type explicitly.
- `--emoji=true|false` overrides the config emoji setting for the command.
- `--test` includes a Pest test file.
- `--js` includes a JavaScript file for multi-file components only.
- `--css` includes CSS files for multi-file components only.
- `php artisan livewire:convert post.create` auto-detects and converts component formats.
- `php artisan livewire:convert post.create --mfc` explicitly converts to multi-file.
- `php artisan livewire:convert post.create --sfc` explicitly converts to single-file.
- The docs warn that test files are deleted when converting multi-file components to single-file format because test files cannot be preserved in the single-file format.

## Choosing A Component Format
- Single-file components are documented as the default, best for most components, easy to understand at a glance, and suited to small or medium components.
- Multi-file components are documented as better for large or complex components, improved IDE support and navigation, and clearer separation when components have significant JavaScript.
- Class-based components are documented for teams migrating from Livewire v2 or v3, teams that prefer a traditional file structure, or teams with established class-based conventions.
- For a new Livewire 4 project, the docs point to single-file or multi-file components for the latest Livewire conventions.

## Component Namespaces
- By default, `pages::` points to `resources/views/pages/`.
- By default, `layouts::` points to `resources/views/layouts/`.
- Additional namespaces can be configured in `config/livewire.php` under `component_namespaces`.
- The docs show `admin` pointing to `resource_path('views/admin')` and `widgets` pointing to `resource_path('views/widgets')` as custom namespace examples.
- Once a namespace is configured, the docs show using it with `php artisan make:livewire admin::users-table`, `<livewire:admin::users-table />`, and `Route::livewire('/admin/users', 'admin::users-table')`.

## Component Locations
- Livewire automatically discovers components in default directories.
- Additional discovery directories can be configured in `config/livewire.php` under `component_locations`.
- The docs show `resource_path('views/components')`, `resource_path('views/admin/components')`, and `resource_path('views/widgets')` as component location examples.

## Programmatic Registration
- In a service provider `boot()` method, register an individual component with `Livewire::addComponent(name: 'custom-button', viewPath: resource_path('views/ui/button.blade.php'))`.
- Register a component directory with `Livewire::addLocation(viewPath: resource_path('views/admin/components'))`.
- Register a namespace with `Livewire::addNamespace(namespace: 'ui', viewPath: resource_path('views/ui'))`.
- For class-based components, register an individual component with `Livewire::addComponent(name: 'todos', class: \App\Livewire\Todos::class)`.
- For class-based components, register a location with `Livewire::addLocation(classNamespace: 'App\\Admin\\Livewire')`.
- For class-based components, register a namespace with `Livewire::addNamespace(namespace: 'admin', classNamespace: 'App\\Admin\\Livewire', classPath: app_path('Admin/Livewire'), classViewPath: resource_path('views/admin/livewire'))`.

## Stubs And Defaults
- Publish customizable component stubs with `php artisan livewire:stubs`.
- Documented single-file stubs include `stubs/livewire-sfc.stub`.
- Documented multi-file stubs include `stubs/livewire-mfc-class.stub`, `stubs/livewire-mfc-view.stub`, `stubs/livewire-mfc-js.stub`, and `stubs/livewire-mfc-test.stub`.
- Documented class-based stubs include `stubs/livewire.stub` and `stubs/livewire.view.stub`.
- Additional documented stubs include `stubs/livewire.attribute.stub` and `stubs/livewire.form.stub`.
- Disable the lightning emoji in `config/livewire.php` with `'make_command' => ['emoji' => false]`.
- Restore v3-style class-based defaults with `'make_command' => ['type' => 'class', 'emoji' => false]`.

## Troubleshooting
- For "Component [post.create] not found" or "Unable to find component" errors, verify the component file path, component name, namespace configuration, and any manual registration.
- For component-not-found errors, the docs also suggest clearing the view cache with `php artisan view:clear`.
- For blank or non-rendering components, documented common causes include a missing root element, syntax errors in the PHP section, and Laravel log errors.
- Livewire requires exactly one root element in a Blade template.
- For duplicate class-name conflicts in single-file components, the docs say to rename one component or namespace one directory.