# Tenancy Configuration

Use this reference after a fresh Context7 lookup for the exact Filament 5 tenancy topic.

## Security Framing
- The docs describe multi-tenancy as one application serving multiple customers, each with separate data and access rules.
- Filament's tenancy system implies a user belongs to many tenants and can switch between them.
- Multi-tenancy is security-sensitive. The docs state that partial or incorrect implementation may expose one tenant's data to another tenant.
- Filament provides tools to help implement tenancy, but the docs explicitly state Filament does not guarantee application security and the application is responsible for being secure.
- If each user only belongs to one tenant, the docs say Filament's many-tenant system may not be needed; observers and global scopes can be used for simpler one-to-many tenancy.

## Setting Up Tenancy
- Specify the tenant model in panel configuration with `tenant(Team::class)`.

```php
use App\Models\Team;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenant(Team::class);
}
```

- Tell Filament which tenants a user belongs to by implementing `Filament\Models\Contracts\HasTenants` on the User model.
- The documented User model example implements both `FilamentUser` and `HasTenants`.
- `getTenants(Panel $panel): Collection` returns the tenants the user belongs to.
- `canAccessTenant(Model $tenant): bool` prevents users from accessing another tenant by guessing a tenant ID in the URL.
- The docs show a many-to-many `teams(): BelongsToMany` relationship and `canAccessTenant()` using `$this->teams()->whereKey($tenant)->exists()`.
- Access the current tenant anywhere in the app with `Filament::getTenant()` using `Filament\Facades\Filament`.

## Tenant Registration and Profile Pages
- Create a tenant registration page by extending `Filament\Pages\Tenancy\RegisterTenant`.
- The page is a full-page Livewire component.
- The documented page implements `public static function getLabel(): string`, `form(Schema $schema): Schema`, and `handleRegistration(array $data): Team`.
- Register the page in panel configuration with `tenantRegistration(RegisterTeam::class)`.
- Create a tenant profile page by extending `Filament\Pages\Tenancy\EditTenantProfile`.
- The documented profile page implements `getLabel()` and `form(Schema $schema): Schema`.
- The docs state profile form data is saved directly to the tenant model.
- Register the profile page with `tenantProfile(EditTeamProfile::class)`.
- The docs say tenant registration/profile base page methods, including `$view`, may be overridden for customization.

## Billing
- Filament provides a billing integration with Laravel Spark.
- Install the Spark billing provider with `composer require filament/spark-billing-provider`.
- Configure Spark billing with `tenantBillingProvider(new SparkBillingProvider())` using `Filament\Billing\Providers\SparkBillingProvider`.
- Require a tenant subscription for any part of the app with `requiresTenantSubscription()`.
- For specific resources and pages, return `true` from `isTenantSubscriptionRequired(Panel $panel): bool`.
- If `requiresTenantSubscription()` is enabled globally, a resource or page may return `false` from `isTenantSubscriptionRequired()` as an exception.
- A custom billing integration implements `Filament\Billing\Providers\Contracts\BillingProvider`.
- The custom billing provider methods are `getRouteAction()` and `getSubscribedMiddleware()`.
- Customize the billing route slug with `tenantBillingRouteSlug('billing')`.

## Tenant Menu
- Add tenant menu items with `tenantMenuItems()`.

```php
use App\Filament\Pages\Settings;
use Filament\Actions\Action;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantMenuItems([
            Action::make('settings')
                ->url(fn (): string => Settings::getUrl())
                ->icon('heroicon-m-cog-8-tooth'),
        ]);
}
```

- Allow tenant menu searching with `searchableTenantMenu()`.
- The docs state tenant menu search is automatically enabled when a user has more than 10 tenants.
- Disable tenant menu search with `searchableTenantMenu(false)`.
- Customize the registration link with the `register` array key: `'register' => fn (Action $action) => $action->label('Register new team')`.
- Customize the profile link with the `profile` array key.
- Customize the billing link with the `billing` array key.
- Tenant menu items are actions and may use documented action methods such as `visible()` and `hidden()` for conditional display.
- Send a `POST` request from a tenant menu item by combining `url()` with `postToUrl()`.
- Disable tenant switching while keeping the menu visible with `tenantSwitcher(false)`.
- Hide the tenant menu with `tenantMenu(false)`; the docs note this is a sign Filament tenancy may not be suitable and simple one-to-many tenancy may be better.

## Tenant Names, Avatars, Defaults, and Labels
- By default, Filament uses the tenant model's `name` attribute.
- Customize the tenant name by implementing `Filament\Models\Contracts\HasName` and `getFilamentName(): string` on the tenant model.
- Customize the tenant avatar URL by implementing `Filament\Models\Contracts\HasAvatar` and `getFilamentAvatarUrl(): ?string` on the tenant model.
- If `getFilamentAvatarUrl()` returns `null`, Filament falls back to `ui-avatars.com`.
- Add a current tenant label by implementing `Filament\Models\Contracts\HasCurrentTenantLabel` and `getCurrentTenantLabel(): string`.
- Set the default tenant after sign-in by implementing `Filament\Models\Contracts\HasDefaultTenant` and `getDefaultTenant(Panel $panel): ?Model` on the user.

## Relationships, Slugs, Routes, and Domains
- For tenant-aware resources, Filament needs an ownership relationship on the resource model and a relationship on the tenant model.
- By default, relationship names are guessed from Laravel conventions. If the tenant model is `App\Models\Team`, Filament looks for `team()` on the resource model. If the resource model is `App\Models\Post`, it looks for `posts()` on the tenant model.
- Customize the ownership relationship globally with `tenant(Team::class, ownershipRelationship: 'owner')`.
- Customize ownership per resource with `protected static ?string $tenantOwnershipRelationshipName = 'owner';`.
- Customize the tenant model's resource relationship per resource with `protected static ?string $tenantRelationshipName = 'blogPosts';`.
- Use a slug in the tenant URL with `tenant(Team::class, slugAttribute: 'slug')`.
- Add a route prefix segment before the tenant with `tenantRoutePrefix('team')` after `path('admin')` and `tenant(Team::class)`; the docs show `/admin/1` becoming `/admin/team/1`.
- Use a domain or subdomain to identify the tenant with `tenantDomain('{tenant:slug}.example.com')` alongside `tenant(Team::class, slugAttribute: 'slug')`.
- Resolve the entire tenant domain with `tenant(Team::class, slugAttribute: 'domain')` and `tenantDomain('{tenant:domain}')`.
- The docs warn that `tenantDomain('{tenant:domain}')` registers a global route parameter pattern for all `tenant` parameters as `[a-z0-9.\-]+`, which may conflict with other panels or app routes using a `tenant` parameter.

## Tenant Middleware and Resource Scoping
- Apply extra middleware to tenant-aware routes with `tenantMiddleware([...])`.
- By default, `tenantMiddleware()` runs on first page load but not subsequent Livewire AJAX requests.
- Make tenant middleware persistent by passing `isPersistent: true`.
- Disable tenancy for one resource with `protected static bool $isScopedToTenant = false;`.
- Opt in to tenancy per resource by calling `Resource::scopeToTenant(false)` in a service provider `boot()` method or middleware, then setting `protected static bool $isScopedToTenant = true;` on resources that should be scoped.

## Tenancy Security Checks
- Tenant-aware resources in a tenancy-enabled panel are automatically scoped to the current tenant for list queries and record route resolution; a user attempting to view a record outside the current tenant receives a 404.
- A tenant-aware resource must exist in the tenancy-enabled panel for its model to receive the automatic global scope.
- Queries made before the tenant is identified, such as from early middleware or a service provider, are not scoped to the current tenant.
- To guarantee middleware runs after the current tenant is identified, register it as tenant middleware.
- Queries outside the tenancy-enabled panel do not have access to the current tenant and are not scoped.
- Disable the tenancy global scope for a specific query with `withoutGlobalScope(filament()->getTenancyScopeName())`.
- If code disables all global scopes, the tenancy global scope is disabled too; the docs warn this can cause data leakage.
- New records for tenant-aware resources are automatically associated with the current tenant by an event listener for the `creating` and `created` events on the resource's Eloquent model.
- A tenant-aware resource must exist in the tenancy-enabled panel for automatic association to happen.
- Models created before the tenant is identified, or outside the tenancy-enabled panel, are not automatically associated with the current tenant.
- If code mutes model events or removes listeners, the docs say to check this is not affecting tenancy.
- Laravel's `unique` and `exists` validation rules do not use Eloquent models by default and therefore do not use global scopes. For complete tenant data separation, the docs recommend `scopedUnique()` and `scopedExists()`.
- To apply additional tenant global scopes to models without resources, create tenant-aware middleware and register it with `tenantMiddleware([ApplyTenantScopes::class], isPersistent: true)`.