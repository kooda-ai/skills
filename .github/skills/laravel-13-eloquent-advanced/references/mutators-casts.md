# Mutators And Casts

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x Eloquent mutators and casts.

## Mutators And Casting Purpose
The docs state accessors, mutators, and attribute casting transform Eloquent attribute values during retrieval or assignment.

The docs mention use cases such as automatic encryption/decryption with Laravel's encrypter and converting JSON strings stored in the database into native PHP arrays.

## Custom Cast Generation
The docs show generating a custom cast class:

```shell
php artisan make:cast AsJson
```

## Custom Cast Implementation
The docs show implementing `CastsAttributes` with `get(...)` and `set(...)` methods:

```php
namespace App\Casts;

use Illuminate\Contracts\Database\Eloquent\CastsAttributes;
use Illuminate\Database\Eloquent\Model;

class AsJson implements CastsAttributes
{
    public function get(Model $model, string $key, mixed $value, array $attributes): array {
        return json_decode($value, true);
    }

    public function set(Model $model, string $key, mixed $value, array $attributes): string {
        return json_encode($value);
    }
}
```

Confirmed imports: `Illuminate\Contracts\Database\Eloquent\CastsAttributes` and `Illuminate\Database\Eloquent\Model`.

## Registering A Custom Cast
The docs show registering a custom cast in a model's `casts()` method:

```php
namespace App\Models;

use App\Casts\AsJson;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected function casts(): array
    {
        return [
            'options' => AsJson::class,
        ];
    }
}
```

## Value Object Casts
The docs show a custom cast class `AsAddress` that converts multiple attributes into an `Address` value object:

```php
<?php

namespace App\Casts;

use App\ValueObjects\Address;
use Illuminate\Contracts\Database\Eloquent\CastsAttributes;
use Illuminate\Database\Eloquent\Model;
use InvalidArgumentException;

class AsAddress implements CastsAttributes
{
    /**
     * Cast the given value.
     *
     * @param  array<string, mixed>  $attributes
     */
    public function get(
        Model $model,
        string $key,
        mixed $value,
        array $attributes,
    ): Address {
        return new Address(
            $attributes['address_line_one'],
            $attributes['address_line_two']
        );
    }

    /**
     * Prepare the given value for storage.
     *
     * @param  array<string, mixed>  $attributes
     * @return array<string, string>
     */
    public function set(
        Model $model,
        string $key,
        mixed $value,
        array $attributes,
    ): array {
        if (! $value instanceof Address) {
            throw new InvalidArgumentException('The given value is not an Address instance.');
        }

        return [
            'address_line_one' => $value->lineOne,
            'address_line_two' => $value->lineTwo,
        ];
    }
}
```

## Encrypted Casting
The docs state encrypted casts automatically encrypt model attribute values using Laravel's built-in encryption features.

The docs state encrypted variants exist for arrays, collections, and objects and function similarly to unencrypted counterparts.

The docs state encrypted text length is unpredictable and usually longer than plain text, so database columns should be `TEXT` or larger.

The docs state encrypted attributes cannot be queried or searched at the database level because they are stored encrypted.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using concrete accessor examples, concrete mutator setter examples, `Attribute` object examples beyond existing references, inbound-only casts, cast parameters, built-in cast lists, enum casts, encrypted cast variant names, array/object/collection cast examples, castable value objects, or cast comparison behavior.
