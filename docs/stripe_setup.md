## Stripe products/prices
- Product: Carousel Maker Pro — Monthly — $15 (Price ID: price_pro_month)
- Product: Carousel Maker Unlimited — Monthly — $29 (Price ID: price_unlimited_month)

## Bubble integration
- Install Bubble Stripe plugin (official). Configure with live and test keys.
- On Billing page, add Subscription element for each plan.
- On subscription created/updated webhook from Stripe (via Bubble or Make):
  - Update User.plan to Pro or Unlimited accordingly.
  - Store stripeCustomerId.
- Free plan is default when user has no active subscription.

## Webhooks
- Stripe → Make or Bubble endpoint: listen to checkout.session.completed, customer.subscription.updated, customer.subscription.deleted
- Update Bubble user plan status accordingly.

## Quotas mapping
- Free: plan=Free, cap=3
- Pro: plan=Pro, cap=30
- Unlimited: plan=Unlimited, cap=9999