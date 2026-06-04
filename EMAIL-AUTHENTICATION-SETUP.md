# Email Authentication Setup Guide
**T-Town Pristine Clean**

Email authentication protects your domain from being used for spam and phishing, and improves deliverability of your own emails.

---

## Why Email Authentication Matters

Without SPF/DKIM/DMARC:
- ❌ Emails go to spam more often
- ❌ Someone can send emails that appear to come from your domain
- ❌ Harder to track email performance
- ❌ Lower trust with email providers

With proper authentication:
- ✅ Emails delivered to inbox (not spam)
- ✅ Your domain protected from spoofing
- ✅ Better email tracking
- ✅ Higher trust score with Gmail, Outlook, etc.

---

## The Three Records You Need

### 1. SPF (Sender Policy Framework)
**What it does:** Tells email providers which servers are authorized to send emails from your domain.

**Simple analogy:** A letter signed "From: J.R. Hart" — SPF verifies that it actually came from J.R., not someone impersonating him.

### 2. DKIM (DomainKeys Identified Mail)
**What it does:** Digitally signs emails to prove they came from your domain and weren't altered in transit.

**Simple analogy:** Signing your signature with a pen — the signature proves authenticity.

### 3. DMARC (Domain-based Message Authentication, Reporting & Conformance)
**What it does:** Tells email providers what to do with emails that fail SPF/DKIM (reject, quarantine, or monitor).

**Simple analogy:** A policy that says "If someone forges my signature, throw out the letter."

---

## Setup Instructions (Namecheap)

Your domain is registered at **Namecheap**. Here's how to add the records.

### Prerequisites
- Admin access to your Namecheap account
- Your domain: `t-townpristineclean.com`
- Current email provider (we'll detect this in steps below)

---

## Step 1: Log In to Namecheap

1. Go to https://www.namecheap.com
2. Click **Sign In** (top right)
3. Log in with your account credentials
4. Click **Account** → **Domain List**
5. Find `t-townpristineclean.com` and click **Manage**

---

## Step 2: Access DNS Records

1. On the domain management page, look for the left sidebar
2. Click **Advanced DNS** (or **DNS Records**)
3. You'll see existing DNS records (you may have some already)

---

## Step 3: Add SPF Record

### What Email Service Are You Using?

**Option A: Formspree (for contact form only)**
Your contact form uses Formspree for submissions. You'll need an email provider for marketing/transactional emails.

**Option B: If you use Google Workspace (Gmail for Business)**
Skip to "SPF for Google Workspace" below.

**Option C: If you use another provider** (SendGrid, Mailgun, Microsoft 365, etc.)
Find your provider's SPF record at the end of this guide.

### SPF for Standard Setup (Formspree + Regular Email)

1. In Namecheap DNS, click **Add Record**
2. Set the following:
   - **Type:** SPF
   - **Name:** @ (leave blank or use @)
   - **Value:** 
   ```
   v=spf1 include:sendgrid.net include:formspree.com ~all
   ```
   - **TTL:** 1800 (or default)

3. Click the **checkmark** to save

**What this does:**
- `v=spf1` — SPF version 1
- `include:sendgrid.net` — Allow SendGrid servers to send (common email provider)
- `include:formspree.com` — Allow Formspree to send form submissions
- `~all` — Soft fail (not strict; some emails may still be delivered even if they fail)

### SPF for Google Workspace (If You Use Gmail for Business)

If you're using Google's email service (Gmail for Business):

1. In Namecheap DNS, click **Add Record**
2. Set:
   - **Type:** SPF
   - **Name:** @
   - **Value:**
   ```
   v=spf1 include:_spf.google.com include:formspree.com ~all
   ```
   - **TTL:** 1800

---

## Step 4: Add DKIM Record

DKIM is more complex because your email provider generates a unique key. Here's how:

### If Using Google Workspace

1. Go to https://admin.google.com
2. Navigate to **Apps** → **Google Workspace** → **Gmail** → **Authenticate email**
3. Click **Create New Record**
4. Google will show you a DKIM record value (looks like: `v=DKIM1; k=rsa; p=MIGfMA0BgQ...`)
5. Go back to Namecheap DNS
6. Click **Add Record**
7. Set:
   - **Type:** CNAME
   - **Name:** `[selector]._domainkey` (Google provides this, e.g., `default._domainkey`)
   - **Value:** Google's value (a long string)
   - **TTL:** 1800
8. Save and verify in Google Admin (may take up to 48 hours)

### If Using SendGrid or Another Provider

Your email provider will give you a DKIM record. Follow the same pattern:
1. Provider gives you a record
2. Add it as CNAME record in Namecheap DNS
3. Verify in your provider's dashboard

**For now:** If you haven't chosen an email provider yet, skip DKIM. SPF is the most critical. You can add DKIM later once you pick an email service.

---

## Step 5: Add DMARC Record

DMARC is the strictest policy. Set it to monitoring first, then make it stricter.

1. In Namecheap DNS, click **Add Record**
2. Set:
   - **Type:** TXT
   - **Name:** `_dmarc`
   - **Value:**
   ```
   v=DMARC1; p=none; rua=mailto:info@t-townpristineclean.com; ruf=mailto:info@t-townpristineclean.com
   ```
   - **TTL:** 1800

3. Save

**What this means:**
- `v=DMARC1` — DMARC version 1
- `p=none` — Don't reject or quarantine; just monitor (safe to start with)
- `rua=` — Send aggregate reports to this email (weekly summary)
- `ruf=` — Send detailed reports on failed emails

### After 1-2 Weeks: Tighten DMARC

Once you've verified SPF/DKIM are working (check your reports), change policy to:

```
v=DMARC1; p=quarantine; rua=mailto:info@t-townpristineclean.com; ruf=mailto:info@t-townpristineclean.com
```

This tells providers to quarantine (spam folder) any emails that fail authentication.

---

## Step 6: Verify Your Records

### Check if Records Were Added

1. Go back to Namecheap Advanced DNS
2. You should see:
   - **SPF record** (type: SPF or TXT)
   - **DMARC record** (type: TXT, name: `_dmarc`)
   - **DKIM record** (type: CNAME, if you set it up)

### Verify SPF is Working

Use a free SPF checker:
1. Go to https://mxtoolbox.com/spf.aspx
2. Enter your domain: `t-townpristineclean.com`
3. Click **Check SPF**
4. You should see: ✅ SPF record found

### Wait for DNS Propagation

DNS changes take **24-48 hours** to fully propagate. Your records may not work immediately.

---

## Common Issues & Solutions

### "No SPF Record Found" (immediately after adding)

**Problem:** DNS hasn't propagated yet.

**Solution:** Wait 24-48 hours and check again. DNS changes take time.

### SPF Record Shows as TXT Instead of SPF

**Problem:** Some DNS providers don't have an SPF type; they use TXT instead.

**Solution:** This is fine. Both work the same way. Some registrars show SPF records as TXT records.

### "Multiple SPF Records Found" Error

**Problem:** You have more than one SPF record.

**Solution:** You can only have ONE SPF record per domain. If you have multiple, delete the old ones and keep only the latest. You can include multiple services in one SPF record (e.g., `v=spf1 include:google.com include:sendgrid.net ~all`).

### Emails Still Going to Spam

**Problem:** SPF/DKIM/DMARC alone don't guarantee inbox delivery.

**Solution:**
1. Check sender reputation (https://www.senderbase.org)
2. Use a real email address (not noreply@)
3. Include unsubscribe link in marketing emails (CAN-SPAM law)
4. Keep email list clean (remove bounces/complaints)
5. Warm up IP address if using dedicated sender

---

## Email Provider Specific SPF Records

Use these if you choose a particular email service:

### Google Workspace (Gmail for Business)
```
v=spf1 include:_spf.google.com ~all
```

### SendGrid
```
v=spf1 include:sendgrid.net ~all
```

### Mailgun
```
v=spf1 include:mailgun.org ~all
```

### Microsoft 365 / Outlook
```
v=spf1 include:protection.outlook.com ~all
```

### Amazon SES
```
v=spf1 include:amazonses.com ~all
```

### Klaviyo (for email marketing)
```
v=spf1 include:klvnhosts.com ~all
```

### HubSpot
```
v=spf1 include:hubspotmail.com ~all
```

**If using multiple services:**
Combine them in one record:
```
v=spf1 include:_spf.google.com include:sendgrid.net include:formspree.com ~all
```

---

## Recommended Email Setup for Small Business

For T-Town Pristine Clean, here's what I recommend:

### Option 1: Google Workspace (Best for Small Teams)
- **Cost:** $6-18/user/month
- **Includes:** Gmail, Drive, Docs, Meet, Calendar
- **SPF:** `v=spf1 include:_spf.google.com ~all`
- **Best for:** Professional email with your domain

### Option 2: Sendgrid or Mailgun (Best for Marketing/Automation)
- **Cost:** $0-30/month (free tier available)
- **Best for:** Transactional emails, newsletters, automated follow-ups
- **SPF:** `v=spf1 include:sendgrid.net ~all`

### Option 3: Hybrid (Google + SendGrid)
- **Gmail** for day-to-day team emails
- **SendGrid** for marketing/automation
- **SPF:** `v=spf1 include:_spf.google.com include:sendgrid.net ~all`

**My recommendation:** Start with Google Workspace ($6/month). You get professional email + all collaboration tools. Add SendGrid later if you need marketing automation.

---

## Testing Your Email Setup

Once you've added SPF/DKIM/DMARC:

### Test 1: Send Email from Your Domain
1. Send an email from your business address (e.g., info@t-townpristineclean.com)
2. Open it in Gmail
3. Click the dropdown arrow next to the sender name
4. Click "Show original"
5. Look for "SPF: PASS" and "DKIM: PASS"

### Test 2: Use a Free Test Tool
- https://www.mail-tester.com (comprehensive email test)
- https://mxtoolbox.com/spf.aspx (SPF checker)
- https://mxtoolbox.com/dmarc.aspx (DMARC checker)

---

## Monitoring & Maintenance

### Monthly Checklist
- [ ] Check DMARC reports (emailed to your address)
- [ ] Review SPF/DKIM status
- [ ] Monitor email deliverability
- [ ] Check for any authentication failures

### Tools to Monitor
- **Google Admin Console** (if using Workspace)
- **SendGrid Dashboard** (if using SendGrid)
- **Namecheap DNS Records** (verify records still exist)

---

## Quick Setup Summary

**For today (minimal setup):**
1. Add SPF record to Namecheap DNS: `v=spf1 include:formspree.com ~all`
2. Add DMARC record: `v=DMARC1; p=none; rua=mailto:info@t-townpristineclean.com`
3. Wait 24-48 hours for DNS to propagate
4. Verify with SPF checker (mxtoolbox.com)

**For next week (full setup):**
1. Choose email provider (Google Workspace recommended)
2. Set up DKIM with your provider
3. Update SPF to include your email provider
4. Tighten DMARC policy from `p=none` to `p=quarantine`

---

## Questions?

- **Namecheap Help:** https://www.namecheap.com/support/
- **SPF Explanation:** https://www.dmarcian.com/spf/
- **DKIM Explanation:** https://www.dmarcian.com/dkim/
- **DMARC Explanation:** https://www.dmarcian.com/dmarc/

**Next steps after email auth is set up:**
1. Set up Google Business Profile (if not done)
2. Configure email follow-up automation (for form submissions)
3. Monitor email deliverability weekly
