# T-Town Pristine Clean — Project Brief (v2)

Single source-of-truth for the rebuild. Drop into a Claude Code session as the project spec.
Workstreams: **(1) Website**, **(2) Security**, **(3) Marketing Automation**, **(4) Monitoring, SEO/GEO & Conversion**.

**Positioning: COMMERCIAL-FIRST.** Commercial cleaning is the primary business and the focus of the site, messaging, SEO, and ads. Residential is offered but secondary.

Business: T-Town Pristine Clean — commercial & residential cleaning, Tulsa OK.
Domain: `t-townpristineclean.com` (registered at Namecheap).
Phone: (539) 233-0353 · Email: info@t-townpristineclean.com · 1726 S Yorktown Ave, Tulsa, OK 74104.
Service area: Tulsa, Sand Springs, Broken Arrow, Owasso, Bixby, Jenks.

---

## 1. Website

### Goal
Replace the compromised WordPress site with a fast, secure, **statically generated** site that reads as professional and sales-driving, **leads with commercial cleaning**, and converts visitors into qualified leads. Same domain.

### Recommended stack
- **Astro** (static-first, zero JS by default, great for content + SEO pages). Alternatives: Eleventy, Next.js static export.
- **Tailwind CSS** for styling tokens.
- Content as **Markdown/MDX** so the automation system can write pages into the repo.
- **Cloudflare Pages** or **Netlify** hosting (free tier fine; automatic HTTPS).
- **Git** as version control + backup.

### Design direction (professional / sleek / B2B-credible)
Move away from playful template aesthetics toward the credibility of a premium commercial-services brand.
- **Palette:** ink/deep-slate base, warm neutral backgrounds, ONE disciplined accent (confident teal or trustworthy blue). No busy multi-color gradients.
- **Typography:** one characterful display face + one clean, legible body face. No default system-font look.
- **Layout:** generous whitespace, strong grid, real photography of actual crews & finished commercial spaces (not stock).
- **Above the fold:** commercial value prop, ONE primary CTA — *Request a Free Walkthrough & Quote* — phone number, and immediate B2B trust signals (insured & bonded, ★ rating, years in business, # of facilities served).
- **Sales drivers:** social proof high on the page, transparent process, risk-reversal/guarantee, repeated quote CTAs.

### Commercial positioning specifics
- Speak to: office/facility managers, property managers, general contractors (post-construction), and operators of medical, dental, retail, churches, schools, multi-unit.
- Foreground B2B needs: COIs/insurance & bonding, consistent vetted crews, after-hours & recurring scheduling, customizable contracts, account management, references.
- **Primary conversion = walkthrough/bid request** (+ phone), not instant online booking.
- Dedicated **industries served** content and commercial case studies/testimonials.

### Page architecture (commercial-led)
- **Home** — commercial value prop, services, industries, process, social proof, service areas, walkthrough CTA.
- **Commercial Cleaning (flagship)** — contracts, scheduling, insurance/bonding, industries, COIs, references.
- **Janitorial / Office Cleaning** · **Post-Construction** · **Medical/Specialty** (as warranted).
- Services hub + pages: Office/Commercial, Post-Construction, Move-In/Move-Out, Deep Cleaning, Recurring.
- **Residential** — present but secondary ("We also clean homes").
- **About** · **Gallery** · **Careers** · **Contact** (walkthrough/quote form) · **Blog** · **Service-area pages** · **Book Online** (embedded scheduler).

### Forms
- Managed form service (Netlify Forms / Formspree / Cloudflare) + honeypot + Turnstile/hCaptcha. No custom server.

### SEO foundations (commercial intent)
- Target: "commercial cleaning Tulsa", "office cleaning Tulsa", "janitorial services Tulsa", "post-construction cleaning Tulsa", + industry/neighborhood combos.
- Per-page titles/meta, OpenGraph/Twitter, canonicals.
- `sitemap.xml`, `robots.txt`, schema.org `LocalBusiness` + `Service`.
- Verify in **Google Search Console** + **Bing Webmaster Tools**.

---

## 2. Security Checklist

A static site removes the database + plugin attack surface that caused the breach. Lock down the rest.

### Hosting & delivery
- [ ] HTTPS everywhere; enable **HSTS**.
- [ ] **Cloudflare** in front: WAF, DDoS, bot mitigation.
- [ ] Headers: `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `Referrer-Policy`, `Permissions-Policy`, `frame-ancestors`.

### Domain (Namecheap)
- [ ] **2FA** on the account.
- [ ] **Registrar lock** + **DNSSEC**.
- [ ] Strong unique password; WHOIS privacy.

### Accounts & secrets
- [ ] 2FA on GitHub, host, email provider, Google accounts.
- [ ] API keys (Anthropic, email, Google) as **env secrets** — never committed.
- [ ] Least-privilege tokens; rotate periodically.

### Email (outreach)
- [ ] **SPF**, **DKIM**, **DMARC** DNS records.

### Operations
- [ ] Git = versioned backup.
- [ ] Uptime + SSL-expiry monitoring.
- [ ] Search Console open for "hacked content" alerts.

### Migration cleanup (one-time)
- [ ] Build the new static site fresh — do NOT import the infected WP DB/files.
- [ ] After launch & verification, decommission old WordPress + unused hosting.
- [ ] Remove all former-contractor admin/FTP access.

---

## 3. Marketing Automation System

### Objective
Generate and assist distribution of marketing content + outreach on a schedule, with **human approval** before anything publishes or sends.

### Architecture (server-less, rides the static workflow)
```
GitHub repo (site + content + automation)
   |- GitHub Actions (scheduled cron)
   |    |- generate:blog         -> drafts/blog/*.md
   |    |- generate:neighborhood -> drafts/areas/*.md
   |    |- generate:seasonal     -> drafts/blog/*.md
   |    |- generate:social       -> drafts/social/*.json
   |    |- gbp:posts             -> drafts/gbp/*.md  (Google Business posts)
   |    |- gbp:review-replies    -> drafts/gbp/replies/*.md (await approval)
   |    |- ads:copy              -> drafts/ads/*.json (ad + landing copy)
   |    |- outreach:reviews      -> queue review-request emails
   |    |- outreach:followup     -> queue follow-up emails
   |- Claude API (generation)
   |- Email provider (Resend / SendGrid)
   |- Google Business Profile API (if access approved)
   |- Google Ads API / Ads Scripts (optional, advanced)
   |- Job/customer data source (CSV / Sheet / booking-tool export)
```
All generated content lands in **`/drafts`** and opens a **Pull Request** → you approve → merge → rebuild/deploy. Nothing goes live unreviewed.

### Config (single source the generator reads)
- `brand.yaml`: voice/tone, do/don't words, services, guarantees, contact info.
- `neighborhoods.yaml`: areas + genuinely distinct local detail (NOT name swaps).
- `industries.yaml`: commercial verticals + their specific cleaning needs.
- `seasons.yaml`: Tulsa seasonal themes/timing.

### Modules
1. **Weekly blog posts** — cron weekly; commercial-leaning topics; MDX w/ title/meta/schema.
2. **Neighborhood + industry SEO pages** — ONE high-quality, distinct page each. *See guardrail.*
3. **Seasonal articles** — Tulsa seasonal timing.
4. **Social snippets** — 3–5 platform-sized posts per blog; queue or push to Buffer/Later.
5. **Google Business Profile** — draft weekly GBP posts + review replies; keep info consistent. *Access caveat below.*
6. **Google Ads** — generate ad copy, headlines, keyword sets, and matching landing pages. *Management caveat below.*
7. **Review requests** — triggered after a completed job; email w/ direct Google review link.
8. **Email follow-ups** — drip: quote-sent-no-booking, post-service thank-you, lapsed-client win-back.

### Google Business Profile — notes
- Highest-leverage local lever; powers local SEO + GEO + conversion.
- **Access caveat:** Google's Business Profile APIs require application + approval. With access → drafts post/auto-with-approval. Without → system drafts content; you paste manually (still a major time-saver).
- Review management (prompt requests + drafted replies) is a double win for ranking and conversion.

### Google Ads — notes
- **Layer 1 (easy, high value):** generate ad copy, keyword lists, and matching landing pages for commercial searches.
- **Layer 2 (advanced):** programmatic management via Google Ads API (needs developer token + approval) or Google Ads Scripts for automated rules/reporting. Start manual + assisted, graduate to API.
- **Strongly consider Local Services Ads (Google Guaranteed):** top placement, pay-per-lead, trust badge — strong for local commercial lead-gen. Less API-automatable; system supports it via reviews + lead tracking.
- Caveats: ads cost money; copy must follow Google Ads policy; a human owns budget/strategy.

### Guardrails (build in — don't skip)
- **SEO quality:** Google's *scaled content abuse* policy penalizes mass thin/duplicate pages. Each page must be genuinely useful + distinct + **human-approved before publish**. Quality over volume.
- **Email compliance (CAN-SPAM):** working **unsubscribe** + **physical address** on every marketing email; honor opt-outs.
- **SMS (if added):** **TCPA consent** required before texting.
- **Brand safety:** review generated content for accuracy (no invented stats/prices/guarantees) before shipping.

### Build phases
1. **Static site (commercial-first) live & replacing the hacked one** — home + commercial flagship + key service pages + contact, behind Cloudflare with security headers.
2. Blog + neighborhood/industry/seasonal templates + content config.
3. Generation modules + GitHub Actions cron + PR approval flow.
4. Outreach (email provider, reviews, follow-ups) with compliance baked in.
5. Google Business Profile + Google Ads modules.
6. Social snippet queue + optional scheduler integration.

---

## 4. Monitoring, SEO/GEO & Conversion (ongoing)

Turns the site into a measurable lead machine.

### Measure
- **GA4** + event tracking on form submits and CTA clicks.
- **Call tracking** so you know which pages/keywords drive phone leads.
- **Google Search Console** + rank tracking for commercial keywords.
- Lead source attribution (organic / GBP / ads / referral).

### SEO / GEO
- **SEO:** technical health, internal linking, fresh commercial content cadence (fed by automation), local citations + consistent NAP.
- **GEO (Generative Engine Optimization):** structure content so AI answer engines (Google AI Overviews, ChatGPT, Perplexity) cite you — clear Q&A blocks, strong structured data, factual consistency across the web, authoritative local + industry content. Reinforces classic local SEO.

### Convert
- Fast load, clear single primary CTA, trust signals, easy walkthrough/quote capture.
- Iterate headlines/CTAs based on data; lightweight A/B via content edits.

### Upkeep loop
- Dashboard/report: traffic, rankings, leads, conversion rate, ad spend vs. leads.
- Scheduled review (weekly/monthly) to act on what's working.

---

## Open inputs needed from owner
- Logo file, brand colors (if any), photos of crews/commercial results.
- Google Business Profile link (for review automation + GBP posts).
- Preferred booking tool and email provider.
- Whether to pursue Google Business Profile API and/or Google Ads API access.
- Confirmation of current admin/hosting access; removal of former-contractor access.
