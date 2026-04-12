# Chapter 7: Post-Launch Ops

Launching is not the finish line. It's the starting line.

Most SaaS products that fail don't fail at launch. They fail in the months after, when the founder is too busy building features to notice that the app is slow, the database is leaking data, or Stripe webhooks are silently failing.

Post-launch ops is the work that keeps your product alive and trustworthy.

## Security: The Work That Never Stops

### Weekly Security Habits

- **Review new database tables for RLS policies**: Every new table needs row-level security. No exceptions. It's easy to forget when you're moving fast.
- **Check for exposed secrets**: Run a scan of your codebase for hardcoded API keys, database URLs, or tokens. Tools like GitGuardian or TruffleHog automate this.
- **Review Supabase auth logs**: Look for unusual patterns: spikes in failed login attempts, signups from disposable email domains, or suspicious IP addresses.

### Monthly Security Habits

- **Update dependencies**: Run `npm audit` and update packages with known vulnerabilities. Don't let them pile up.
- **Review API endpoints**: Are any endpoints missing authentication checks? Are any returning more data than they should?
- **Test your backup restoration**: Having backups is not enough. You need to verify you can actually restore from them.

### The Security Checklist You Can't Skip

- [ ] RLS policies on every table, including new ones added after launch
- [ ] No service role keys in client-side code
- [ ] Rate limiting on all public endpoints
- [ ] Webhook signature verification on all incoming webhooks
- [ ] HTTPS everywhere, no mixed content warnings

## Monitoring: Know Before Your Users Do

### What to Monitor

- **Uptime**: Is your app responding? Set up ping monitoring with 1-minute intervals.
- **Response time**: Are pages loading in under 2 seconds? Slow apps lose users quietly.
- **Error rate**: What percentage of requests return errors? Anything above 1% needs investigation.
- **Webhook delivery**: Are Stripe webhooks succeeding? Failed webhooks mean missed payments and confused users.
- **Database performance**: Are any queries taking more than 500ms? Slow queries compound as your user base grows.

### The Monitoring Stack

| Tool | What It Watches |
|------|----------------|
| **Sentry** | Application errors, stack traces, breadcrumbs showing what the user did before the error |
| **UptimeRobot / Better Stack** | Is your app up? Alerts you via email, SMS, or Slack within 60 seconds of downtime |
| **PostHog** | User behavior, feature adoption, conversion funnels |
| **Supabase Dashboard** | Database performance, query stats, storage usage |

You don't need all of these on day one. Start with Sentry (errors) and uptime monitoring. Add the rest as your user count grows.

## Performance: The Silent Killer

Users don't complain about slow apps. They just leave. Here's what to optimize and when:

### Optimize Immediately (Before It Becomes a Problem)

- **Image optimization**: Serve images in WebP format, use Next.js Image component for automatic resizing and lazy loading.
- **Bundle size**: Run `next build` and check the output. Any page chunk over 200KB needs attention.
- **Database indexes**: Add indexes on columns you filter or sort by frequently. A missing index turns a 10ms query into a 2-second query.

### Optimize When You Hit 100+ Users

- **Caching**: Add caching headers for static assets. Consider Redis for frequently accessed data.
- **Connection pooling**: Database connections are expensive. Use a connection pooler (Supabase includes one via PgBouncer) to share connections across requests.
- **Edge functions**: Move latency-sensitive operations closer to users by deploying them at the edge.

### Optimize When You Hit 1,000+ Users

- **CDN for static assets**: Vercel handles this by default. If you're self-hosting, set up CloudFront or Cloudflare.
- **Background jobs**: Move any operation that takes more than 2 seconds out of the request path and into a background queue. Inngest or similar tools handle this well.
- **Database read replicas**: When your primary database is handling too many read queries, add a replica.

## The Post-Launch Toolkit

[Build This Now](https://www.buildthisnow.com) includes 14 post-launch commands specifically for this phase: security scanning, penetration testing, performance optimization, dependency auditing, error triage, and continuous monitoring. If you're using it, these ops tasks become one-command operations instead of manual checklists.

For everyone else, build the habits described above and automate what you can. The founders who stay in business are the ones who treat post-launch ops as part of the product, not an afterthought.

## The One Rule

If you remember nothing else from this chapter: set up error tracking and uptime monitoring before you launch. Everything else can wait. But if your app goes down and you don't know about it, you'll lose users you'll never get back.

Next up: [Chapter 8: Scaling as a Solo Founder](08-scaling-as-solo-founder.md)
