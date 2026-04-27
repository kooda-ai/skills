# Factory States and Relationships

## State Methods
The Eloquent factories docs show custom state methods built with `state(...)`:

```php
use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * Indicate that the user is suspended.
 */
public function suspended(): Factory
{
    return $this->state(function (array $attributes) {
        return [
            'account_status' => 'suspended',
        ];
    });
}
```

## Factory Callbacks
The docs show configuring callbacks with `configure()`, `afterMaking(...)`, and `afterCreating(...)`:

```php
namespace Database\Factories;

use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;

class UserFactory extends Factory
{
    /**
     * Configure the model factory.
     */
    public function configure(): static
    {
        return $this->afterMaking(function (User $user) {
            // ...
        })->afterCreating(function (User $user) {
            // ...
        });
    }

    // ...
}
```

The docs also show combining callbacks inside a state method:

```php
use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * Indicate that the user is suspended.
 */
public function suspended(): Factory
{
    return $this->state(function (array $attributes) {
        return [
            'account_status' => 'suspended',
        ];
    })->afterMaking(function (User $user) {
        // ...
    })->afterCreating(function (User $user) {
        // ...
    });
}
```

## Has-Many Relationships
The Eloquent factories docs show child relationship creation with `has(...)`:

```php
use App\Models\Post;
use App\Models\User;

$user = User::factory()
    ->has(Post::factory()->count(3))
    ->create();
```

```php
$user = User::factory()
    ->has(Post::factory()->count(3), 'posts')
    ->create();
```

```php
$user = User::factory()
    ->has(
        Post::factory()
            ->count(3)
            ->state(function (array $attributes, User $user) {
                return ['user_type' => $user->type];
            })
    )
    ->create();
```

## Belongs-To Relationships
The docs show parent relationship creation with `for(...)`:

```php
use App\Models\Post;
use App\Models\User;

$posts = Post::factory()
    ->count(3)
    ->for(User::factory()->state([
        'name' => 'Jessica Archer',
    ]))
    ->create();
```

```php
$user = User::factory()->create();

$posts = Post::factory()
    ->count(3)
    ->for($user)
    ->create();
```

## Many-to-Many and Pivot Attributes
The docs show `hasAttached(...)` for many-to-many relationships with pivot attributes:

```php
use App\Models\Role;
use App\Models\User;

$user = User::factory()
    ->hasAttached(
        Role::factory()->count(3),
        ['active' => true]
    )
    ->create();
```

The docs also show magic relationship helpers:

```php
$user = User::factory()
    ->hasRoles(1, [
        'name' => 'Editor'
    ])
    ->create();
```

## Recycling Existing Related Models
The docs show `recycle(...)` for reusing existing model instances:

```php
Ticket::factory()
    ->recycle(Airline::factory()->create())
    ->create();
```

```php
Ticket::factory()
    ->recycle($airlines)
    ->create();
```

## Boundaries
- Run a fresh lookup before using exact `Sequence` code, polymorphic relationship factory helpers beyond the returned `hasAttached(...)` example, `forUser()` magic method examples, or advanced callback typing beyond the returned snippets.
- Do not infer unsupported relationship helper names from naming conventions alone.
