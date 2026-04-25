# Tenancy Users

Use this reference after a fresh Context7 lookup for the exact Filament 5 tenant-user, tenant access, tenant menu, billing, or tenancy security topic.

## Security Framing
- Filament's tenancy features automatically scope tenant-aware resources in a tenancy-enabled panel.
- The docs warn that custom queries, actions, pages, validation, and code outside the tenancy-enabled panel must be handled carefully to prevent unauthorized data access.
- If a task involves tenancy, state the security assumptions and verify whether the code is inside a tenancy-enabled panel.

## Tenant Model and User Access
- Register the tenant model in panel configuration with `tenant()`:

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
- `getTenants(Panel $panel): Collection` returns the user's tenants.
- `canAccessTenant(Model $tenant): bool` prevents users from accessing another tenant by guessing a tenant ID in the URL.

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Models\Contracts\HasTenants;
use Filament\Panel;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Support\Collection;

class User extends Authenticatable implements FilamentUser, HasTenants
{
    // ...

    public function teams(): BelongsToMany
    {
        return $this->belongsToMany(Team::class);
    }

    public function getTenants(Panel $panel): Collection
    {
        return $this->teams;
    }

    public function canAccessTenant(Model $tenant): bool
    {
        return $this->teams()->whereKey($tenant)->exists();
    }
}
```

- Access the current tenant with:

```php
use Filament\Facades\Filament;

$tenant = Filament::getTenant();
```

- Set the default tenant after sign-in by implementing `HasDefaultTenant` on the User model.

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Models\Contracts\HasDefaultTenant;
use Filament\Models\Contracts\HasTenants;
use Filament\Panel;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;

class User extends Model implements FilamentUser, HasDefaultTenant, HasTenants
{
    // ...

    public function getDefaultTenant(Panel $panel): ?Model
    {
        return $this->latestTeam;
    }

    public function latestTeam(): BelongsTo
    {
        return $this->belongsTo(Team::class, 'latest_team_id');
    }
}
```

## Tenant Registration and Profile Pages
- Create a tenant registration page by extending `Filament\Pages\Tenancy\RegisterTenant`.
- The documented page implements `getLabel()`, `form(Schema $schema): Schema`, and `handleRegistration(array $data): Team`.

```php
namespace App\Filament\Pages\Tenancy;

use App\Models\Team;
use Filament\Forms\Components\TextInput;
use Filament\Pages\Tenancy\RegisterTenant;
use Filament\Schemas\Schema;

class RegisterTeam extends RegisterTenant
{
    public static function getLabel(): string
    {
        return 'Register team';
    }

    public function form(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('name'),
                // ...
            ]);
    }

    protected function handleRegistration(array $data): Team
    {
        $team = Team::create($data);

        $team->members()->attach(auth()->user());

        return $team;
    }
}
```

```php
use App\Filament\Pages\Tenancy\RegisterTeam;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantRegistration(RegisterTeam::class);
}
```

- Create a tenant profile page by extending `Filament\Pages\Tenancy\EditTenantProfile`.

```php
namespace App\Filament\Pages\Tenancy;

use Filament\Forms\Components\TextInput;
use Filament\Pages\Tenancy\EditTenantProfile;
use Filament\Schemas\Schema;

class EditTeamProfile extends EditTenantProfile
{
    public static function getLabel(): string
    {
        return 'Team profile';
    }

    public function form(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('name'),
                // ...
            ]);
    }
}
```

- Register the tenant profile page with `tenantProfile(EditTeamProfile::class)` after confirming the current Context7 lookup includes it.

## Tenant Identity
- Filament uses the tenant model's `name` attribute by default.
- Customize tenant display by implementing `HasName` and `getFilamentName()` on the tenant model.

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\HasName;
use Illuminate\Database\Eloquent\Model;

class Team extends Model implements HasName
{
    // ...

    public function getFilamentName(): string
    {
        return "{$this->name} {$this->subscription_plan}";
    }
}
```

- Customize the current tenant switcher label with `HasCurrentTenantLabel` and `getCurrentTenantLabel()`.

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\HasCurrentTenantLabel;
use Illuminate\Database\Eloquent\Model;

class Team extends Model implements HasCurrentTenantLabel
{
    // ...

    public function getCurrentTenantLabel(): string
    {
        return 'Active team';
    }
}
```

- Customize tenant avatars by implementing `HasAvatar` and `getFilamentAvatarUrl(): ?string` on the tenant model.

## Tenant Menu
- Add tenant menu items with `tenantMenuItems()` and `Filament\Actions\Action`.

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
            // ...
        ]);
}
```

- Customize the tenant profile link with the `profile` array key.

```php
use Filament\Actions\Action;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantMenuItems([
            'profile' => fn (Action $action) => $action->label('Edit team profile'),
            // ...
        ]);
}
```

- Enable tenant menu search with `searchableTenantMenu()`.
- Disable tenant switching but keep the menu visible with `tenantSwitcher(false)`.
- Hide the tenant menu with `tenantMenu(false)`.

## Tenant Routes, Domains, and Relationships
- Customize the ownership relationship globally with `tenant(Team::class, ownershipRelationship: 'owner')`.
- Customize ownership per resource with `protected static ?string $tenantOwnershipRelationshipName = 'owner';`.
- Customize the tenant model relationship per resource with `protected static ?string $tenantRelationshipName = 'blogPosts';`.
- Use a slug in tenant URLs with `tenant(Team::class, slugAttribute: 'slug')`.
- Add a tenant route prefix with `tenantRoutePrefix('team')`.

```php
use App\Models\Team;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->path('admin')
        ->tenant(Team::class)
        ->tenantRoutePrefix('team');
}
```

- Use tenant domains or subdomains with `tenantDomain()`:

```php
use App\Models\Team;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenant(Team::class, slugAttribute: 'slug')
        ->tenantDomain('{tenant:slug}.example.com');
}
```

```php
use App\Models\Team;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenant(Team::class, slugAttribute: 'domain')
        ->tenantDomain('{tenant:domain}');
}
```

## Tenant Middleware and Resource Scoping
- Apply middleware to tenant-aware routes with `tenantMiddleware([...])`.
- Make tenant middleware persistent across Livewire AJAX requests with `isPersistent: true`.

```php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantMiddleware([
            // ...
        ], isPersistent: true);
}
```

- Disable tenancy for one resource with `protected static bool $isScopedToTenant = false;`.
- Disable automatic tenancy scoping globally with `Resource::scopeToTenant(false)` and opt in per resource with `protected static bool $isScopedToTenant = true;`.
- Tenant-aware resources in a tenancy-enabled panel are automatically scoped for list queries, editing, viewing, and record route resolution; users attempting to access records outside the current tenant receive a 404.
- Use `scopedUnique()` and `scopedExists()` for form validation queries that should respect global scopes and multi-tenancy.

```php
use Filament\Forms\Components\TextInput;

TextInput::make('email')
    ->scopedUnique()
    // or
    ->scopedExists()
```

## Tenant Billing
- Install the Spark billing provider with:

```bash
composer require filament/spark-billing-provider
```

- Register Spark billing with `tenantBillingProvider(new SparkBillingProvider())`.

```php
use Filament\Billing\Providers\SparkBillingProvider;
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantBillingProvider(new SparkBillingProvider());
}
```

- Require a tenant subscription panel-wide with `requiresTenantSubscription()`.
- For resources or pages, implement `isTenantSubscriptionRequired(Panel $panel): bool` and return `true`; if the global requirement is enabled, returning `false` creates an exception.
- Customize the billing route slug with `tenantBillingRouteSlug('billing')`.
- Customize the tenant menu billing link with the `billing` array key after confirming the current Context7 lookup includes the billing link topic.
- A custom billing provider implements `Filament\Billing\Providers\Contracts\BillingProvider` with `getRouteAction()` and `getSubscribedMiddleware()`.
