# Auth Page Customization Boundary

The Users docs confirm the customization pattern, but Context7 may return different levels of detail depending on the query.

## Confirmed Pattern
- Create a custom Filament page class.
- Extend the relevant base auth page class from Filament.
- Override methods such as `form()` when the current lookup confirms them.
- Pass the custom page class to the relevant panel configuration method.

## Directly Confirmed Example
- `App\Filament\Pages\Auth\EditProfile` extends `Filament\Auth\Pages\EditProfile as BaseEditProfile`.
- The custom page overrides `form(Schema $schema): Schema`.
- The example uses `TextInput::make('username')`, `getNameFormComponent()`, `getEmailFormComponent()`, `getPasswordFormComponent()`, and `getPasswordConfirmationFormComponent()`.
- The custom page is registered with `profile(EditProfile::class)`.

## Required Re-Query
Before writing concrete code for custom login, registration, password reset, or email verification pages, run a narrower Context7 query for that specific page and include only the base class and helpers returned by the docs.
