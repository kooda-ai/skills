# Wave Blade Directives

## Documented Directives
- `@auth`
- `@guest`
- `@admin`
- `@subscriber`
- `@notsubscriber`
- `@subscribed('Plan Name')`
- `@home`

## Documented Usage Notes
- `@auth` checks whether the user is authenticated.
- `@guest` checks whether the user is not authenticated.
- `@admin` checks whether the user is logged in and is an admin.
- `@subscriber` checks whether the authenticated user is a subscriber.
- `@notsubscriber` checks whether the user is not a subscriber.
- `@subscribed('Plan Name')` checks whether a user is subscribed to a specific plan.
- The docs say `@subscribed()` expects the full plan name.
- The docs say `@else` may be used with these directive conditions.
