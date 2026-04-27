# Request Lifecycle

Sources used: Current Laravel 13.x documentation page for request lifecycle.

## Entry Point
The docs state the entry point for all requests to a Laravel application is `public/index.php`.

The docs explain that `public/index.php` loads the Composer-generated autoloader and retrieves an instance of the Laravel application from `bootstrap/app.php`.

## Kernels
The docs state the incoming request is sent to either the HTTP kernel or the console kernel using `handleRequest()` or `handleCommand()` on the application instance, depending on the request type.

The docs identify the HTTP kernel as an instance of `Illuminate\Foundation\Http\Kernel`.

The docs state the HTTP kernel defines an array of bootstrappers that run before the request is executed. These bootstrappers configure error handling, configure logging, detect the application environment, and perform other setup tasks.

The docs also state the HTTP kernel passes the request through the application's middleware stack.

## Service Providers
The docs describe loading service providers as one of the most important kernel bootstrapping actions.

The docs state Laravel iterates through the provider list and instantiates each provider. After providers are instantiated, the `register()` method is called on all providers. Once all providers have been registered, the `boot()` method is called on each provider.

The docs explain that this ordering allows service providers to depend on every container binding being registered by the time `boot()` executes.

The docs state user-defined and third-party service providers used by the application can be found in `bootstrap/providers.php`.

## Routing And Middleware Flow
The docs state that once the application has been bootstrapped and all service providers have been registered, the `Request` is handed off to the router for dispatching.

The docs state the router dispatches the request to a route or controller and runs route-specific middleware.

The docs explain that if the request passes through the matched route middleware, the route or controller method executes and the returned response is sent back through the route's middleware chain.

## Finishing The Response
The docs state the response travels back outward through middleware, giving the application a chance to modify or examine the outgoing response.

The docs then state the HTTP kernel's `handle` method returns the response to `handleRequest()` on the application instance, and `handleRequest()` calls the response object's `send()` method to send the response content to the browser.

## Focus On Providers
The docs emphasize that service providers are the key to bootstrapping a Laravel application and that `AppServiceProvider` is a natural place to add application bootstrapping and service-container bindings.

## Topics Requiring Fresh Lookup
Run a new documentation lookup before describing exact bootstrapper class lists, internal kernel source behavior, exception pipeline internals, Octane-specific lifecycle behavior, console lifecycle details beyond `handleCommand()`, or middleware internals beyond the documented high-level flow.