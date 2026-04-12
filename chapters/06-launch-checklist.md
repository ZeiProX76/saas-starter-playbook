# Chapter 6: Launch Checklist

Your product works locally. Now you need to make sure it works for everyone else.

This checklist covers the things that separate a side project from a real product. Skip these and you'll spend your first week of "launch" fixing embarrassing bugs instead of talking to customers.

## Pre-Launch: Infrastructure

- [ ] **Custom domain configured**: yourdomain.com, not your-app.vercel.app
- [ ] **SSL certificate active**: Every page loads over HTTPS. No exceptions.
- [ ] **Environment variables set for production**: Database URLs, API keys, and secrets are using production values, not development/test keys
- [ ] **Database backups enabled**: Automated daily backups. Supabase does this by default on paid plans.
- [ ] **Error tracking installed**: Sentry or similar. You need to know when things break before your users tell you.
- [ ] **Uptime monitoring active**: A service like UptimeRobot or Better Stack that pings your app every minute and alerts you when it goes down.

## Pre-Launch: Security

- [ ] **Row-level security enabled on all tables**: Every database table has RLS policies. No user can access another user's data.
- [ ] **No API keys in client-side code**: Check your browser's network tab. If you can see a secret key in the JavaScript bundle, attackers can too.
- [ ] **Rate limiting on auth endpoints**: Prevent brute-force login attempts. 5 attempts per minute per IP is a reasonable default.
- [ ] **Input validation on all forms**: Validate on both client and server. Client-side validation is for user experience. Server-side validation is for security.
- [ ] **CORS configured correctly**: Only your domain should be allowed to make API requests to your backend.
- [ ] **Webhook signatures verified**: If you're using Stripe webhooks (you should be), verify the signature on every webhook to prevent spoofing.

## Pre-Launch: Payments

- [ ] **Stripe in live mode**: Switch from test keys to live keys. Double-check by making a real $1 purchase and refunding it.
- [ ] **Webhook endpoint registered in Stripe dashboard**: Point it to your production URL.
- [ ] **Cancel flow works**: Users can cancel their subscription through your app. Test this.
- [ ] **Failed payment handling**: What happens when a card is declined? The user should see a clear error message, not a blank screen.
- [ ] **Receipt emails sending**: Payment confirmation emails go out automatically after every charge.

## Pre-Launch: User Experience

- [ ] **Signup flow tested end-to-end**: New email, signup, email verification, login, complete core action. The whole thing, start to finish.
- [ ] **Mobile responsive**: Test on a real phone, not just browser dev tools. Pay attention to forms and tables.
- [ ] **Loading states on all async actions**: Every button that triggers a network request should show a spinner or loading state. No silent waiting.
- [ ] **Error messages are helpful**: "Something went wrong" is not helpful. "Your email is already registered. Try logging in instead." is helpful.
- [ ] **Empty states designed**: What does a new user see before they have any data? A blank page with no guidance is a churn machine.

## Pre-Launch: Legal

- [ ] **Privacy policy published**: Required by law in most jurisdictions. Include what data you collect, how you use it, and how users can request deletion.
- [ ] **Terms of service published**: Basic terms covering acceptable use, liability limits, and refund policy.
- [ ] **Cookie consent (if needed)**: Required if you serve users in the EU and use analytics or tracking cookies.

## Pre-Launch: Analytics

- [ ] **Analytics installed**: PostHog, Mixpanel, or even simple Plausible. You need to know what users are doing.
- [ ] **Key events tracked**: At minimum: signup, login, core action completed, payment completed, cancellation. These are your funnel.
- [ ] **Conversion funnel defined**: Visitor > Signup > Activation > Payment. Know your numbers from day one.

## Launch Day

- [ ] **Share on 3+ channels**: Product Hunt, Indie Hackers, Reddit (r/SaaS, r/SideProject), X, LinkedIn. Don't launch quietly.
- [ ] **Respond to every comment within 2 hours**: Early engagement determines whether platforms boost your visibility.
- [ ] **Monitor error tracking dashboard**: Watch for spikes in errors as new users hit edge cases you didn't test.
- [ ] **Check payment webhooks are processing**: Verify in Stripe dashboard that webhooks are delivering and being acknowledged.

## The 80/20 Rule of Launching

You will never feel ready. The checklist above covers the essentials, not everything. Ship when the critical items are done. Polish after launch.

If you want a head start on most of these checklist items, build systems like [Build This Now](https://www.buildthisnow.com) handle security, payments, error tracking, and analytics configuration out of the box. That lets you focus your pre-launch energy on product quality and launch distribution instead of infrastructure.

Next up: [Chapter 7: Post-Launch Ops](07-post-launch-ops.md)
