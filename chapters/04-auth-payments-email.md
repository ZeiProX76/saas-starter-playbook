# Chapter 4: Auth, Payments, Email

These three systems are the least exciting parts of any SaaS product. They're also the ones that will sink you if you get them wrong.

Nobody signs up for your product because you have great authentication. But if your auth is broken, they leave and never come back. Same for payments and email.

## Authentication

### What You Need on Day One

- Email/password signup and login
- Password reset flow
- Session management (keeping users logged in)
- Protected routes (pages only logged-in users can see)

### What You'll Need Soon After

- OAuth login (Google, GitHub, etc.)
- Magic link login (passwordless)
- Email verification
- Rate limiting on login attempts

### The Critical Mistake: Building Auth Yourself

Don't do it. Use Supabase Auth, Auth0, Clerk, or a similar service. Here's why:

- Password hashing, token management, and session security have dozens of subtle vulnerabilities. One mistake and you're leaking user data.
- OAuth implementations change constantly. Google alone has updated their OAuth flow three times in the past two years.
- Auth edge cases are endless: expired tokens, concurrent sessions, account linking, email changes. You'll spend weeks handling them.

Supabase Auth gives you all of the above for free, with row-level security policies that protect your database at the query level.

### Row-Level Security: Non-Negotiable

Row-level security (RLS) means every database query is automatically filtered so users can only see their own data. Without it, one bad API endpoint can expose user A's data to user B.

This is not a "nice to have." It's a requirement. Set it up before you write your first feature.

## Payments

### What You Need on Day One

- A checkout page that accepts credit cards
- Webhook handling to confirm successful payments
- At least one pricing plan (keep it simple: one plan, monthly billing)

### What You'll Need Soon After

- Annual billing option
- Customer portal (users can update payment method, cancel, view invoices)
- Free trial or freemium tier
- Usage-based billing (if your model requires it)

### Use Stripe. Don't Overthink This.

Stripe handles subscriptions, one-time payments, invoices, tax collection, and customer management. Its webhook system tells your app when payments succeed, fail, or cancel.

The integration pattern:

1. Create a Stripe checkout session on your backend
2. Redirect the user to Stripe's hosted checkout page
3. Stripe sends a webhook to your server when payment completes
4. Your server updates the user's subscription status in your database

This flow works for 99% of SaaS products. Don't build a custom checkout page until you have a specific reason.

### Critical Payments Mistakes

- **Not handling failed webhooks**: Webhooks can fail. You need retry logic and idempotency keys.
- **Storing payment status only in Stripe**: Always mirror subscription status in your own database. Stripe API calls add latency to every auth check.
- **Launching without a cancel flow**: If users can't cancel, you'll get chargebacks. Chargebacks can get your Stripe account suspended.

## Email

### What You Need on Day One

- Welcome email after signup
- Payment confirmation email
- Password reset email

### What You'll Need Soon After

- Onboarding sequence (3 to 5 emails over the first week)
- Usage notifications ("Your trial expires in 3 days")
- Transactional receipts (monthly billing confirmations)

### The Stack: Resend + React Email

Resend handles delivery. React Email lets you build templates with React components, so your emails look consistent with your app.

The key metric: deliverability. Your emails need to land in inboxes, not spam folders. To ensure this:

- Set up SPF, DKIM, and DMARC records on your domain
- Send from a subdomain (mail.yourdomain.com) to protect your main domain's reputation
- Keep your email volume consistent. Sudden spikes trigger spam filters.

## The Build-vs-Buy Decision

All three of these systems (auth, payments, email) follow the same logic: buy the infrastructure, build the product-specific parts.

Every hour you spend building auth from scratch is an hour you're not spending on the feature that makes your product unique. Tools like [Build This Now](https://www.buildthisnow.com) come with auth, Stripe payments, and email already integrated and working. You configure them with your own API keys and start building product features immediately.

The boring infrastructure should be solved on day one, not day thirty.

Next up: [Chapter 5: AI-Powered Development](05-ai-powered-development.md)
