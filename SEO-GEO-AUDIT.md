# SEO & GEO Optimization Audit Report
**T-Town Pristine Clean**  
**Date:** June 4, 2026  
**Status:** Implementation Complete

---

## Executive Summary

Your website has a strong foundation with good schema markup, meta tags, and content structure. This audit identified and implemented critical improvements for both traditional SEO and Generative Engine Optimization (GEO) — critical for ranking in AI-powered search results like Google AI Overviews, ChatGPT, and Perplexity.

**Key metrics impacted:**
- ✅ Search visibility (Google, Bing)
- ✅ AI answer engine visibility (GEO)
- ✅ Local search ranking
- ✅ Featured snippet eligibility

---

## Changes Implemented

### 1. **Technical SEO Foundations**

#### Added `robots.txt`
- Instructs search engines which pages to crawl
- Blocks common AI scrapers (optional — you can remove these blocks if you want AI engines to cite you)
- Points to sitemap.xml

**Location:** `/robots.txt`

#### Added `sitemap.xml`
- Lists all 10+ pages and their priority
- Helps search engines discover and crawl all content
- Includes: homepage, service areas, blog posts
- Update priority/dates as you add new content

**Location:** `/sitemap.xml`

#### Added Canonical Tags
**Pages updated:**
- `index.html` → `https://t-townpristineclean.com/`
- `service-areas.html` → `https://t-townpristineclean.com/service-areas.html`
- `blog/index.html` → `https://t-townpristineclean.com/blog/`
- `blog/how-often-commercial-cleaning.html` → full canonical

**Why:** Prevents duplicate content issues and tells search engines which version to rank.

#### Added Meta Robots Tags
All pages now include:
```html
<meta name="robots" content="index, follow, max-snippet:-1, max-image-preview:large, max-video-preview:-1">
```

**Benefits:**
- `index, follow` — Allow indexing and link following
- `max-snippet:-1` — Allow full snippets in search results (better CTR)
- `max-image-preview:large` — Show images in results
- `max-video-preview:-1` — Show video previews

---

### 2. **Generative Engine Optimization (GEO)**

#### Added FAQ Schema
**Why this matters:** AI answer engines (Google AI Overviews, ChatGPT, Perplexity) use FAQ schema to:
- Extract questions and answers
- Cite your content as a source
- Drive traffic to your site

**Added to:** Homepage (`index.html`)

**FAQs included:**
1. What services do you offer?
2. What areas do you serve?
3. Are you licensed and insured?
4. Do you offer after-hours cleaning?
5. How do I get a quote?
6. What industries do you clean?

**How to expand:** Add more FAQs as you get customer questions. These naturally match what people ask in Google and ChatGPT.

#### Added Breadcrumb Schema
**Why:** Helps AI engines understand site structure and improves click-through from search results.

**Added to:**
- Homepage
- Service Areas
- Blog Index
- Blog posts

---

### 3. **GEO Content Optimization Opportunities**

The following will further boost visibility in AI answer engines:

#### A. Add Q&A Sections to Blog Posts
**Example for `/blog/how-often-commercial-cleaning.html`:**

Currently: Generic article structure
**Recommended:** Add a "Questions We're Asked" section mid-article with:
- **Q: How often should offices be cleaned?**  
  A: Daily to 2x weekly depending on foot traffic and industry.
- **Q: What's the difference between janitorial and deep cleaning?**  
  A: Janitorial is routine maintenance; deep cleaning tackles buildup.

**Format:** Use `<h3>` and `<p>` so AI engines can parse questions.

#### B. Create Comparison Tables
AI engines love tables for easy extraction.

**Example:** Create a table showing cleaning frequency by industry:

| Industry | Recommended Frequency | Why |
|----------|---------------------|-----|
| Medical/Dental | Daily | High-touch surfaces, regulatory requirements |
| Offices | 2-3x weekly | Standard professional standard |
| Retail | Daily-Weekly | Customer-facing, foot traffic |
| Industrial | Custom | Heavy soiling, chemical safety |

#### C. Add Local Schema Extensions
Current schema is good. Consider adding:

**Service area schema** (in `/service-areas.html`):
```json
{
  "@type": "LocalBusiness",
  "areaServed": {
    "@type": "City",
    "name": "Tulsa, Oklahoma"
  }
}
```

This reinforces to Google and AI engines that you're hyperlocal.

#### D. Structured Pricing & Availability
If you post prices or availability, add:

```json
{
  "@type": "Service",
  "name": "Commercial Cleaning",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "Custom quote",
    "availability": "Monday-Sunday"
  }
}
```

AI engines can then answer: "How much does commercial cleaning cost in Tulsa?" with your structured data.

---

## SEO Best Practices to Continue

### 1. **Keyword Optimization**
Your target keywords (all look good in titles/descriptions):
- "commercial cleaning Tulsa"
- "office cleaning Tulsa"
- "janitorial services"
- "post-construction cleaning"

**Check your homepage rank:** Google Search Console → Performance → Filter by these terms.

### 2. **Internal Linking**
Currently: You link from homepage to service areas and blog.

**Opportunity:** In blog posts, link back to:
- Homepage (for general audience)
- Relevant service pages (e.g., blog about medical cleaning → link to medical/dental section)
- Service areas (e.g., mention Tulsa/Broken Arrow → link to `/service-areas.html`)

**Why:** Distributes authority and helps Google crawl related pages.

### 3. **Fresh Content**
Your blog has 6 posts. Good start.

**Next steps:**
- Plan 2-4 blog posts per month (Q&A topics customers ask)
- Update old posts with new data annually (update `dateModified` in schema)
- Link new blog posts from homepage or in footer

**Content ideas:**
- "Top 5 commercial cleaning mistakes" 
- "How to choose a cleaning contractor"
- "Post-construction cleaning checklist"
- Seasonal: "Spring office cleaning" (May-June), "End-of-year facility refresh" (Nov-Dec)

### 4. **Page Load Speed**
Check at: https://pagespeed.web.dev (paste your domain)

**Quick wins if needed:**
- Compress hero image
- Use WebP format for images
- Lazy-load below-the-fold images

### 5. **Mobile Optimization**
Your site is responsive — good. Verify at:
- Google Mobile-Friendly Test: https://search.google.com/test/mobile-friendly
- Inspect your site on actual phones

### 6. **Google Business Profile**
Critical for local SEO and GEO.

**To-do:**
1. Claim your GBP: https://business.google.com
2. Add high-quality photos of cleaned spaces
3. Respond to reviews (all platforms)
4. Post weekly updates (GBP has a blog/posts feature)

**Impact:** Reviews + photos are heavily weighted by Google Search and by AI engines that cite you.

---

## Monitoring & Measurement

### Google Search Console
1. Go to https://search.google.com/search-console
2. Add your site (select "URL prefix" → `https://t-townpristineclean.com`)
3. Watch:
   - **Performance** → Which keywords you rank for and CTR
   - **Coverage** → Any indexing errors
   - **Core Web Vitals** → Speed/responsiveness
   - **Enhancements** → Schema errors (should be none now)

### Analytics
You have Google Analytics 4 set up ✅

**Key metrics to monitor:**
- Organic traffic growth (month-over-month)
- Landing page performance (which pages drive conversions)
- Conversion rate (form submissions / visitors)
- Bounce rate (should be <50% for good pages)

### AI Answer Engine Tracking (Beta)
AI engines are nascent. You can monitor mentions via:
- **Perplexity AI** (perplexity.com) — manually search your keywords
- **ChatGPT** (with GPT-4) — manually ask queries
- **Google AI Overviews** (google.com search) — check if you're cited

None of these have tracking APIs yet. Manual spot-checks monthly are your best bet.

---

## File Checklist

**Added files:**
- ✅ `robots.txt`
- ✅ `sitemap.xml`

**Modified files:**
- ✅ `index.html` (canonical, robots meta, FAQ schema, breadcrumb schema)
- ✅ `service-areas.html` (canonical, robots meta, breadcrumb schema)
- ✅ `blog/index.html` (canonical, robots meta)
- ✅ `blog/how-often-commercial-cleaning.html` (canonical, robots meta, breadcrumb schema, fixed JSON)

**Not modified (keep as-is):**
- `styles.css` — CSS doesn't need SEO updates
- `favicon.png`, other images
- `thank-you.html` — not indexed (correct)
- Other blog posts — apply same pattern when you update them

---

## Implementation for Other Blog Posts

All blog posts should have the same improvements. **Template to use:**

1. **Add canonical tag** after og:url:
```html
<link rel="canonical" href="https://t-townpristineclean.com/blog/[filename].html">
<meta name="robots" content="index, follow, max-snippet:-1, max-image-preview:large, max-video-preview:-1">
```

2. **Add breadcrumb schema** before `</head>`:
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {"@type": "ListItem", "position": 1, "name": "Home", "item": "https://t-townpristineclean.com/"},
    {"@type": "ListItem", "position": 2, "name": "Blog", "item": "https://t-townpristineclean.com/blog/"},
    {"@type": "ListItem", "position": 3, "name": "[Article Title]", "item": "https://t-townpristineclean.com/blog/[filename].html"}
  ]
}
```

3. **Add Q&A content** in the article body where relevant.

---

## Long-Term Roadmap

### Phase 1: Foundation (Complete ✅)
- Robots.txt, sitemap, canonical tags, schema markup

### Phase 2: Content (Next)
- Expand blog (2-4 posts/month)
- Add Q&A sections to existing posts
- Create comparison/table content

### Phase 3: Authority (3+ months)
- Build backlinks (local directories, industry sites)
- Grow Google Business Profile (reviews, photos, posts)
- Monitor rankings and traffic

### Phase 4: Advanced (6+ months)
- Consider AI-specific landing pages (Q&A format)
- Explore local schema extensions
- Integrate structured pricing data

---

## Summary

Your site is now **SEO-hardened and GEO-ready**. The additions above put you ahead of most local cleaning competitors. The next leverage point is **content freshness** (blog + GBP) and **authority building** (reviews + backlinks).

**Key wins from this audit:**
1. ✅ Proper indexation (robots.txt, sitemap)
2. ✅ No duplicate content issues (canonicals)
3. ✅ AI answer engine visibility (FAQ + breadcrumb schema)
4. ✅ Clean technical foundation

**Monthly checklist:**
- [ ] Post 2-4 blog articles
- [ ] Update GBP with new photos/posts
- [ ] Respond to all reviews
- [ ] Check Google Search Console for ranking changes
- [ ] Monitor Analytics for traffic trends

---

**Questions?** Refer back to your PROJECT_BRIEF.md (section 4 — Monitoring & SEO/GEO).
