# Social Media & Facebook Pixel Setup Guide
**T-Town Pristine Clean**

---

## Facebook Pixel Integration

Your Facebook Pixel code is now installed. To activate it:

### Step 1: Create a Facebook Business Account (if you don't have one)
1. Go to https://business.facebook.com
2. Sign up or log in
3. Create a Business Account for T-Town Pristine Clean

### Step 2: Set Up Your Pixel
1. In Facebook Business Manager, go to **Events Manager**
2. Click **Connect Data Sources** → **Web**
3. Select **Facebook Pixel**
4. Create a new pixel for your website
5. Copy your **Pixel ID** (a long number like `123456789`)

### Step 3: Update Your Website
1. Find this line in your `index.html` (around line 23):
```
fbq('init', 'YOUR_PIXEL_ID_HERE'); // Replace YOUR_PIXEL_ID_HERE with your Facebook Pixel ID
```

2. Replace `YOUR_PIXEL_ID_HERE` with your actual Pixel ID. Example:
```
fbq('init', '1234567890123456');
```

3. Also replace `YOUR_PIXEL_ID_HERE` in the noscript tag below:
```
<img ... src="https://www.facebook.com/tr?id=1234567890123456&ev=PageView&noscript=1" />
```

4. Save and deploy. Your pixel is now tracking!

### What Your Pixel Tracks
- **Page Views** — Every visitor to your site
- **Form Submissions** — When someone requests a walkthrough
- **User behavior** — Pages they visit, time on site, etc.

### Using Your Pixel for Ads
Once your pixel has tracked ~100 website visitors:
1. Go to **Ads Manager** (facebook.com/ads)
2. Create a new campaign
3. Choose **Conversions** or **Lead Generation** as your objective
4. Your pixel automatically shows audiences and conversions

---

## Social Media Profile Links

Your footer now has social media icons (Facebook, Instagram, LinkedIn, X/Twitter). Here's how to update them with your actual profiles:

### Step 1: Create Your Social Media Accounts (if you don't have them)

**Facebook Business Page:**
1. Go to https://www.facebook.com
2. Create a Business Page for "T-Town Pristine Clean"
3. Copy your page URL (e.g., `https://www.facebook.com/TtownPristineClean`)

**Instagram:**
1. Go to https://www.instagram.com
2. Create a business account for "T-Town Pristine Clean"
3. Copy your profile URL (e.g., `https://www.instagram.com/ttownpristineclean`)

**LinkedIn Company Page:**
1. Go to https://www.linkedin.com
2. Create a **Company Page** (not a personal profile)
3. Copy your company page URL (e.g., `https://www.linkedin.com/company/t-town-pristine-clean`)

**X (formerly Twitter):**
1. Go to https://twitter.com
2. Create an account for "T-Town Pristine Clean" 
3. Copy your profile URL (e.g., `https://twitter.com/TtownClean`)

### Step 2: Update Your Website Footer

In your `index.html`, find the social media links section in the footer (around line 370):

```html
<a href="https://www.facebook.com" title="Facebook" ...>
<a href="https://www.instagram.com" title="Instagram" ...>
<a href="https://www.linkedin.com" title="LinkedIn" ...>
<a href="https://twitter.com" title="X (Twitter)" ...>
```

Replace each `href` with your actual profile URL:

**Before:**
```html
<a href="https://www.facebook.com" title="Facebook" ...>
```

**After (example):**
```html
<a href="https://www.facebook.com/TtownPristineClean" title="Facebook" ...>
```

**All four links to update:**
- Facebook: `https://www.facebook.com/YOUR_PAGE_NAME`
- Instagram: `https://www.instagram.com/YOUR_HANDLE`
- LinkedIn: `https://www.linkedin.com/company/YOUR_COMPANY_NAME`
- X: `https://twitter.com/YOUR_HANDLE`

### Step 3: Test Your Links
1. Deploy your changes
2. Go to your website and scroll to the footer
3. Click each social icon — it should open your profile in a new tab

---

## Content Strategy for Social Media

Once your accounts are set up, here's what to post:

### Facebook Business Page (1-2x per week)
- Before/after photos of cleaned spaces
- Customer testimonials
- Tips about commercial cleaning
- Event announcements (grand opening, anniversary, etc.)
- Link to blog posts

**Engagement tip:** Respond to all comments and messages within 24 hours. Facebook's algorithm favors active business pages.

### Instagram (3-5x per week)
- Instagram Stories with quick cleaning tips
- Reels showing time-lapse cleaning
- Before/after carousel posts
- Team photos
- Customer spotlights

**Instagram strategy:** Use relevant hashtags like `#CommercialCleaning`, `#TulsaCleaning`, `#CleaningServices`, etc.

### LinkedIn (2x per week)
- Industry insights and thought leadership
- Company updates and milestones
- Articles about workplace health/cleanliness
- Team spotlights
- Share blog posts

**LinkedIn approach:** More professional tone. Target facility managers and business owners.

### X/Twitter (3-5x per week)
- Quick tips and industry news
- Engage with local Tulsa accounts
- Share blog posts
- Respond to local cleaning/business tweets
- Join relevant conversations

---

## Connecting Social to Your Marketing

### Google Business Profile
Add your social media links to your Google Business Profile:
1. Go to https://business.google.com
2. Edit your business info
3. Add links to your Facebook, Instagram, and website

### Email Signature
Add social icons to your business email signature so clients can follow you.

### Blog Posts
At the end of each blog post, encourage readers to:
- Follow you on social media
- Like/share the post
- Join your email list

---

## Measuring Social Media Impact

**Key metrics to track:**
- **Followers** — Growth month-over-month
- **Engagement** — Likes, comments, shares per post
- **Website traffic** — How many social clicks bring people to your site
- **Leads** — DMs or inquiries from social media

**Tools to use:**
- **Facebook:** Built-in Insights (free)
- **Instagram:** Built-in Insights (free)
- **LinkedIn:** Built-in Analytics (free)
- **X/Twitter:** Analytics (free for business accounts)
- **Google Analytics:** Track which social posts drive site traffic

---

## Timeline for Social Media Launch

**Week 1:**
- [ ] Create accounts on all 4 platforms
- [ ] Update website with links
- [ ] Set up Facebook Pixel
- [ ] Add profile photos and bios

**Week 2-3:**
- [ ] Create 10-15 initial posts for each platform
- [ ] Schedule posts for the next month
- [ ] Invite team members and past clients to follow

**Week 4+:**
- [ ] Maintain 2-5 posts per week per platform
- [ ] Respond to comments and DMs daily
- [ ] Link social posts to blog content
- [ ] Monitor analytics weekly

---

## Pro Tips

1. **Consistency beats perfection** — Post regularly even if content isn't polished
2. **Use your phone** — Smartphone photos are authentic and perform well on social
3. **Behind-the-scenes content** — Show your team at work, before/afters, company culture
4. **Testimonial posts** — Share customer quotes with permission and tag them
5. **Local hashtags** — Use #Tulsa, #TulsaCleaning, #TowntownTulsa, etc.
6. **Cross-promote** — Tell your email list about social, mention social in blog posts
7. **Engage others** — Comment on local Tulsa businesses' posts to build relationships

---

## Next Steps

1. Set up your accounts and add profile links (this week)
2. Install Facebook Pixel ID once you create your Business account
3. Plan your first month of content
4. Schedule posts consistently
5. Monitor performance monthly

Questions? Refer back to this guide or check each platform's help center.
