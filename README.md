# T-Town Pristine Clean — Website

Static, commercial-first website for T-Town Pristine Clean (Tulsa, OK). No database, no plugins — fast and secure by design.

## Contents
```
index.html        # the full single-page site
styles.css        # all styles
images/           # logo + real photos (replace with real job photos over time)
PROJECT_BRIEF.md  # full project plan: site, security, automation, monitoring
```

## Run locally
Just open `index.html` in a browser, or serve the folder:
```
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Deploy (pick one — both free, both give automatic HTTPS)

### Option A — Cloudflare Pages
1. Push this folder to a new GitHub repo.
2. Cloudflare dashboard → Pages → Connect to Git → select the repo.
3. Build command: *(none)* · Output directory: `/`
4. Add your domain `t-townpristineclean.com` in Pages → Custom domains, and update the DNS at Namecheap as prompted.

### Option B — Netlify
1. Push to GitHub (or drag-and-drop the folder at app.netlify.com).
2. Connect the repo; no build command needed.
3. Domain settings → add `t-townpristineclean.com`; point Namecheap DNS to Netlify.

## Make the "Request a Walkthrough" form actually email you
The form currently shows a success message via JS (demo only). To send real submissions to **info@t-townpristineclean.com**, do ONE of the following.

### If hosting on Netlify (easiest)
In `index.html`, wrap the form fields in a real form tag and add `name` attributes:
```html
<form name="walkthrough" method="POST" data-netlify="true" netlify-honeypot="bot-field">
  <input type="hidden" name="form-name" value="walkthrough">
  <p hidden><input name="bot-field"></p>
  <!-- add name="..." to each input/select/textarea, e.g. name="business" -->
  ...
  <button type="submit" class="btn btn-primary">Request My Walkthrough</button>
</form>
```
Then in Netlify → Forms → Notifications, send submissions to info@. Remove the `onclick`/JS demo.

### If hosting on Cloudflare Pages (use Formspree)
1. Create a form at formspree.io, get your endpoint (e.g. `https://formspree.io/f/abc123`).
2. Set the form to `action="https://formspree.io/f/abc123" method="POST"` and add `name` attributes to fields.
3. Formspree emails each submission to info@.

## Security checklist (see PROJECT_BRIEF.md for the full list)
- [ ] Enable Cloudflare in front (WAF, HTTPS, HSTS).
- [ ] Add security headers (CSP, X-Content-Type-Options, Referrer-Policy, Permissions-Policy).
- [ ] Namecheap: enable 2FA, registrar lock, DNSSEC.
- [ ] Do NOT migrate anything from the old hacked WordPress install — this is a clean build.

## To-do before / shortly after launch
- [ ] Replace `images/owner.jpg` with a real photo of J.R. (current one is a placeholder).
- [ ] Swap stock/representative photos for real job photos as you collect them.
- [ ] Confirm exact Google rating + review count (currently shown as 5.0).
- [ ] Update Google Business Profile primary category to "Commercial cleaning service" / "Janitorial service" to match the commercial positioning.
- [ ] Keep name/address/phone identical across the site, Google, Yelp, Nextdoor, Thumbtack.

## Next phase: marketing automation
See `PROJECT_BRIEF.md` (sections 3 & 4) for the content + outreach engine: scheduled blog/SEO/seasonal content, social snippets, Google Business posts, review requests, and email follow-ups — all built to run on GitHub Actions with a human-approval step.
