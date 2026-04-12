# Chapter 2: Tech Stack Decisions

Your tech stack is a bet. Pick wrong and you'll spend weeks migrating. Pick right and you'll barely think about infrastructure for the first two years.

Here's what matters for a SaaS MVP: speed to ship, production readiness, and a clear upgrade path. Everything else is noise.

## The Stack That Works

After watching hundreds of SaaS products launch (and fail), the pattern is clear. The stack that gets MVPs to market fastest while staying production-ready:

| Layer | Pick | Why |
|-------|------|-----|
| **Frontend** | Next.js + React | Server-side rendering, API routes, massive ecosystem. Most SaaS products use this for a reason. |
| **Styling** | Tailwind CSS + shadcn/ui | Fast prototyping, consistent design, 50+ polished components you own. |
| **Database** | PostgreSQL via Supabase | Enterprise-grade database with built-in auth, row-level security, and real-time subscriptions. Free tier supports two projects. |
| **Auth** | Supabase Auth | Email/password, Google login, magic links, password reset. All working out of the box. |
| **Payments** | Stripe | Subscriptions, one-time charges, customer portal, webhooks. Industry standard. |
| **Email** | Resend + React Email | Transactional email with React-based templates. Reliable delivery, clean developer experience. |
| **Hosting** | Vercel | One-click deploys from GitHub, global CDN, auto-scaling. Free tier for getting started. |

This is not the only valid stack. But it's battle-tested, well-documented, and every piece has a generous free tier.

## Decisions That Don't Matter Yet

New founders waste weeks debating things that are irrelevant at the MVP stage:

- **Microservices vs. monolith**: You're a monolith. You'll be a monolith for a long time. That's fine.
- **Which state management library**: Start with React's built-in state. Add complexity only when you feel the pain.
- **SQL vs. NoSQL**: Use PostgreSQL. It handles both relational and JSON data. Decision made.
- **Self-hosted vs. managed**: Use managed services. You're building a product, not managing servers.

## Decisions That Actually Matter

### Type Safety

Use TypeScript. Not optional. A type-safe API layer (from database to frontend) catches entire categories of bugs before they reach production. Tools like oRPC with Zod give you end-to-end type safety with minimal boilerplate.

### Row-Level Security

Your database needs row-level security (RLS) from day one. Without it, one API bug can expose every user's data to every other user. Supabase makes RLS straightforward with policy templates.

This is not something you can bolt on later. Build it in from the start.

### Auth and Payments: Build or Buy?

Buy. Always buy. Every founder who builds auth from scratch regrets it within six months. Same for payments. Stripe and Supabase Auth are better than anything you'll build yourself, and they're battle-tested by millions of users.

If you want a stack where auth, payments, database security, and email are already wired together and working, [Build This Now](https://www.buildthisnow.com) ships with all of this pre-integrated. It saves roughly 395+ hours of the infrastructure work described above.

## The "Can I Change This Later?" Test

Before committing to any technology, ask: how hard is it to swap out?

- **Easy to change**: UI components, styling framework, email provider, analytics tool
- **Medium effort**: Hosting provider, error tracking, background job runner
- **Painful to change**: Database, auth provider, payment processor, programming language

Spend your decision-making energy on the painful-to-change items. For everything else, pick something reasonable and move on. Perfectionism at this stage is just procrastination with better branding.

Next up: [Chapter 3: MVP in 48 Hours](03-mvp-in-48-hours.md)
