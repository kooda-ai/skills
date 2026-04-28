---
name: wave-billing-subscriptions
description: 'Use when: working with Wave billing, Stripe setup in Wave, Paddle setup in Wave, BILLING_PROVIDER, Stripe and Paddle webhook routes, subscription plans, plan-role association, Price IDs, and Wave subscription-related access patterns confirmed by the docs. Requires Context7 /websites/devdojo_wave docs before adding details.'
argument-hint: 'Wave billing provider, Stripe/Paddle setup, plan setup, or subscription task'
---

# Wave Billing And Subscriptions

## Purpose
Use this skill for documented Wave billing setup with Stripe or Paddle, subscription plan setup, and plan-to-role relationships.

## Source Rule
1. Before giving final billing or subscription guidance, query Context7 for `/websites/devdojo_wave` with the exact Wave topic.
2. Do not add env vars, webhook paths, handled events, customer portal behavior, testing steps, plan fields, or Price ID guidance unless they appear in the current Wave docs.
3. If the task needs deeper Stripe or Paddle product behavior beyond what Wave documents, say that clearly and query the provider docs separately.
4. Keep examples close to documented env vars, endpoints, and admin flows.

## Reference Map
- Billing providers, webhook setup, test hooks, plans, and plan-role linkage: [providers-webhooks-and-plans.md](./references/providers-webhooks-and-plans.md)

## Related Wave Skills
- Use `wave-access-control-admin` for the documented role and permission side of plan-based access control.
- Use `wave-auth-users` for subscriber-facing auth flows, profile settings, and user access surfaces around subscriptions.
- Use `wave-content-api` when billing questions overlap with API key access or user-facing content areas rather than provider setup.

## Workflow
1. Identify whether the task is provider selection, Stripe setup, Paddle setup, webhook debugging, plan setup, or Price ID mapping.
2. Run a narrow Context7 query for `/websites/devdojo_wave`.
3. Load the reference file above.
4. Use only the documented Wave provider config, webhook, and admin plan flows.
5. Preserve the documented relationship between plans and roles.
6. Omit payment-provider behavior not confirmed by the Wave docs.

## Confirmed Core Patterns
- Wave billing uses `BILLING_PROVIDER` in `.env` and stores the value in `config/wave.php`.
- The docs say the billing provider may be `stripe` or `paddle`.
- Stripe setup uses `STRIPE_PUBLISHABLE_KEY`, `STRIPE_SECRET_KEY`, and `STRIPE_WEBHOOK_SECRET`.
- The Stripe webhook endpoint is documented as `/webhook/stripe`.
- The docs warn that checkout can succeed while the account stays unupgraded if the webhook is not configured correctly.
- The docs show local Stripe webhook testing with `stripe listen --forward-to https://wave.test/webhook/stripe`.
- Paddle setup includes `PADDLE_ENV`, `PADDLE_VENDOR_ID`, `PADDLE_API_KEY`, and `PADDLE_CLIENT_SIDE_TOKEN`.
- The Paddle webhook path is documented as `webhook/paddle`.
- The documented Paddle events handled by Wave are `subscription.cancelled`, `subscription.created`, `subscription.updated`, and `transaction.payment_failed`.
- The Paddle default payment link in the docs is `http://yourdomain.com/settings/subscription`.
- Default subscription plans are Basic, Premium, and Pro.
- The docs say plans are linked to roles and users receive the role associated with the plan they purchase.
- The plan docs recommend keeping plan names and role names lowercase.
- Stripe Price IDs come from Stripe product prices and are pasted into the plan Price ID field in Wave admin.
- Paddle price IDs come from Paddle catalog prices and are pasted into the plan Price ID field in Wave admin.

## Completion Check
- A fresh Context7 lookup for `/websites/devdojo_wave` was used for the exact billing or subscription topic.
- Every env var, webhook path, event name, plan relationship, and admin flow is traceable to the current Wave docs.
- Deeper Stripe or Paddle behavior is not inferred beyond what the Wave docs confirm.
