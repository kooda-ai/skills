# Plugin Concepts

Use this reference after a fresh Context7 lookup for the exact Filament 5 Plugins topic.

## Plugin Contexts
- Filament provides a plugin system for adding app-specific functionality or redistributable packages that other developers can include.
- The docs describe two main contexts: Panel Plugins and Standalone Plugins.
- Panel Plugins are used with Panel Builders and are typically used only inside a panel or as a complete panel in themselves.
- Panel Plugin examples include dashboard widgets and sets of resources or functionality, such as a Blog or User Management feature.
- Standalone Plugins are used outside a Panel Builder.
- Standalone Plugin examples include custom form fields, table columns, and table filters.
- The docs state these contexts can be used together inside the same plugin and do not have to be mutually exclusive.

## Plugin Object
- Filament introduces a Plugin object used to configure a plugin.
- The Plugin object is a simple PHP class implementing `Filament\Contracts\Plugin`.
- The docs describe this class as the main entry point for plugin configuration.
- The docs state the Plugin object is also used to register resources and icons that might be used by the plugin.
- The Plugin object is not required to build a plugin.
- The Plugin object is only used for Panel Providers.
- Standalone Plugins do not use the Plugin object; their configuration should be handled in the plugin service provider.

## Assets
- The docs state all asset registration, including CSS, JavaScript, and Alpine components, should be done through the plugin service provider in `packageBooted()`.
- Asset registration allows Filament to register assets with the Asset Manager and load them when needed.
- For exact asset APIs, query Context7 for the Filament 5 asset-management topic and load the Filament 5 Configuration or Styling skill before writing code.

## Creating a Plugin
- The docs recommend using the Filament Plugin Skeleton to start a plugin.
- The documented skeleton workflow is to use the GitHub template, clone the repository, navigate to the project root, and run:

```bash
php ./configure.php
```

- The docs state the configure script asks questions, stubs out a new plugin, and prepares the extension for development.

## Upgrading Existing Plugins
- The docs state there is no one-size-fits-all upgrade approach because plugin scope and functionality vary.
- A consistent upgrade note is the deprecation of `PluginServiceProvider`.
- The docs show changing the plugin service provider to extend `PackageServiceProvider`.
- The docs show adding a static `$name` property used to register the plugin with Filament.

```php
class MyPluginServiceProvider extends PackageServiceProvider
{
    public static string $name = 'my-plugin';

    public function configurePackage(Package $package): void
    {
        $package->name(static::$name);
    }
}
```

- Do not add extra package-tool methods, publishing behavior, command registration, migrations, routes, views, translations, or asset code unless a fresh lookup confirms the requested details.