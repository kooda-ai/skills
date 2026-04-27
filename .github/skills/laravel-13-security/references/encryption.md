# Encryption

Sources used: Context7 `/websites/laravel_13_x` results for Laravel 13.x encryption.

## Configuration
The docs state Laravel's encrypter requires the `key` configuration option in `config/app.php`.

The docs state this configuration value is driven by the `APP_KEY` environment variable.

The docs state `php artisan key:generate` should be used to generate the `APP_KEY` value because it uses PHP's secure random bytes generator to build a cryptographically secure key.

The docs state the `APP_KEY` value is typically generated during Laravel installation.

## Encrypting Strings
The docs show encrypting a string with the `Crypt` facade:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Crypt;

class DigitalOceanTokenController extends Controller
{
    /**
     * Store a DigitalOcean API token for the user.
     */
    public function store(Request $request): RedirectResponse
    {
        $request->user()->fill([
            'token' => Crypt::encryptString($request->token),
        ])->save();

        return redirect('/secrets');
    }
}
```

Confirmed import: `Illuminate\Support\Facades\Crypt`.

The docs state encrypted values are encrypted using OpenSSL and the AES-256-CBC cipher.

The docs state encrypted values are signed with a message authentication code (MAC), preventing decryption of values tampered with by malicious users.

## Decrypting Strings
The docs show decrypting a string and handling tampered or invalid-key data:

```php
use Illuminate\Contracts\Encryption\DecryptException;
use Illuminate\Support\Facades\Crypt;

try {
    $decrypted = Crypt::decryptString($encryptedValue);
} catch (DecryptException $e) {
    // ...
}
```

Confirmed imports: `Illuminate\Contracts\Encryption\DecryptException` and `Illuminate\Support\Facades\Crypt`.

The docs state `DecryptException` occurs if data is tampered with or the key is invalid.

## Graceful Key Rotation
The docs show configuring current and previous encryption keys in `.env`:

```ini
APP_KEY="base64:J63qRTDLub5NuZvP+kb8YIorGS6qFYHKVo6u7179stY="
APP_PREVIOUS_KEYS="base64:2nLsGFGzyoae2ax3EF2Lyq/hH6QghBGLIq5uL+Gp8/w="
```

The docs state changing `APP_KEY` logs out all authenticated users because Laravel encrypts every cookie, including session cookies.

The docs state data encrypted with a previous key cannot be decrypted after changing `APP_KEY` unless previous keys are configured.

The docs state `APP_PREVIOUS_KEYS` may contain a comma-delimited list of previous encryption keys.

The docs state Laravel encrypts values with the current key, but during decryption it tries the current key first, then previous keys until one can decrypt the value.

## Topics Requiring Fresh Lookup
Run a new Context7 query before using object or array encryption APIs, `encrypt()` / `decrypt()` examples, cipher configuration, serialized payload behavior, key rotation automation, custom encrypters, or encryption behavior in cookies/sessions beyond the statements returned here.