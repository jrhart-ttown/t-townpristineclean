# Email Authentication — Quick Start (30 Minutes)

Do this today to fix the SPF record issue.

---

## What You Need

- Namecheap login
- 15 minutes
- No technical knowledge required

---

## The 5-Minute Version

### Step 1: Go to Namecheap DNS
1. Log in at https://www.namecheap.com
2. Click **Account** → **Domain List**
3. Find `t-townpristineclean.com` → click **Manage**
4. Click **Advanced DNS**

### Step 2: Add SPF Record
1. Click **Add Record**
2. Fill in:
   - Type: SPF
   - Name: @ (or leave blank)
   - Value: `v=spf1 include:formspree.com ~all`
   - TTL: 1800
3. Click checkmark to save

### Step 3: Add DMARC Record
1. Click **Add Record**
2. Fill in:
   - Type: TXT
   - Name: `_dmarc`
   - Value: `v=DMARC1; p=none; rua=mailto:info@t-townpristineclean.com`
   - TTL: 1800
3. Click checkmark to save

### Step 4: Verify (24-48 hours later)
1. Go to https://mxtoolbox.com/spf.aspx
2. Enter: `t-townpristineclean.com`
3. Click **Check SPF**
4. Should show ✅ SPF record found

**Done!** Your SPF record is now live.

---

## What These Do

- **SPF:** Tells email providers your emails are legitimate (not spam)
- **DMARC:** Sets policy for emails that fail checks

---

## Next Steps (Do Later)

1. **Set up professional email** (Google Workspace, $6/month)
   - Replaces info@ email with Gmail
   - Adds DKIM automatically
   
2. **Update SPF if you add email service**
   - Current: `v=spf1 include:formspree.com ~all`
   - With Google: `v=spf1 include:_spf.google.com ~all`

3. **Monitor DMARC reports**
   - Check `info@t-townpristineclean.com` once a week for reports
   - These show which emails passed/failed authentication

---

## Troubleshooting

### "I can't find Advanced DNS"
- Make sure you clicked **Manage** for the right domain
- Look for "DNS Records" or "Advanced DNS" in the left sidebar
- If still stuck: https://www.namecheap.com/support/

### "SPF record not found" (right after adding)
- Wait 24-48 hours — DNS is still updating
- Then check again at mxtoolbox.com

### Multiple SPF Records Error
- Delete the old one
- Keep only the new one

---

## That's It!

Your SPF record is now set up. Email will be more reliable and secure.

For detailed instructions, see `EMAIL-AUTHENTICATION-SETUP.md`.
