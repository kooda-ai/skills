# Providers, Webhooks, And Plans

## Billing Provider Selection
- Billing provider selection uses `BILLING_PROVIDER` in `.env` and is stored in `config/wave.php`.
- The docs say the provider may be `stripe` or `paddle`.

## Stripe
- Stripe setup uses `STRIPE_PUBLISHABLE_KEY`, `STRIPE_SECRET_KEY`, and `STRIPE_WEBHOOK_SECRET`.
- The Stripe webhook endpoint is `/webhook/stripe`.
- The docs warn that checkout can succeed while the account stays unupgraded if the webhook is not configured correctly.
- Local Stripe webhook testing is documented with:

```bash
stripe listen --forward-to https://wave.test/webhook/stripe
```

## Paddle
- Paddle setup includes `PADDLE_ENV`, `PADDLE_VENDOR_ID`, `PADDLE_API_KEY`, and `PADDLE_CLIENT_SIDE_TOKEN`.
- The Paddle webhook path is `webhook/paddle`.
- The documented handled events are `subscription.cancelled`, `subscription.created`, `subscription.updated`, and `transaction.payment_failed`.
- The documented default payment link is `http://yourdomain.com/settings/subscription`.

## Plans
- Default plans are Basic, Premium, and Pro.
- Plans are linked to roles, and users receive the role associated with the plan they purchase.
- The docs recommend keeping plan names and role names lowercase.
- Stripe and Paddle price IDs are copied into the plan Price ID field in Wave admin.
