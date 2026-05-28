# Beyond's TMS & POD Tracker — Deployment Guide v3.0

## Architecture (How Cross-Device Sync Works)

```
Admin creates trip → Saved to JSONBin cloud → Bin ID in WhatsApp URL
Rider opens link  → Fetches trip from cloud → Fills POD → Writes back to cloud
Admin refreshes   → Fetches all bins → Sees completed PODs with photos + signature
```

---

## Step 1 — Get a Free JSONBin Account

1. Go to **https://jsonbin.io** → Sign Up (free)
2. After login → click **API Keys** in the top menu
3. Copy your **Master Key** (starts with `$2b$10$...`)
4. Keep it — you'll paste it into the app

---

## Step 2 — Upload Files to GitHub

1. Go to **https://github.com** → Sign In → **"+" → New repository**
2. Repository name: `beyonds-tms`
3. Visibility: **Public** ← required for free GitHub Pages
4. Click **"Create repository"**
5. Click **"uploading an existing file"** → drag and drop all 4 files:
   - `index.html`
   - `admin.html`
   - `pod.html`
   - `DEPLOY.md`
6. Click **"Commit changes"**

---

## Step 3 — Enable GitHub Pages

1. In your repo → **Settings** → **Pages** (left sidebar)
2. Source: **Deploy from a branch**
3. Branch: **main** → Folder: **/ (root)** → **Save**
4. Wait 3–5 minutes → site is live

Your URLs:
```
Admin:  https://YOUR_USERNAME.github.io/beyonds-tms/admin.html
Rider:  https://YOUR_USERNAME.github.io/beyonds-tms/pod.html  (auto-opened via WhatsApp)
```

---

## Step 4 — First-Time Setup in Admin

1. Open `https://YOUR_USERNAME.github.io/beyonds-tms/admin.html`
2. You'll see the **Setup Screen** (one time only)
3. Paste your **JSONBin Master Key**
4. Enter your **GitHub Pages URL**: `https://YOUR_USERNAME.github.io/beyonds-tms`
5. Click **"Save & Launch"**

That's it. The app is live and connected.

---

## Step 5 — Full Workflow Test

1. Admin → **New Trip** → fill details → **Generate Trip + WhatsApp Link**
2. Click **"Open WhatsApp"** → message sent to rider with link
3. Rider opens link on mobile → completes 7-step POD flow:
   - Pickup photos
   - Delivery photos *(mandatory — can't close without)*
   - Stamped invoice photo *(mandatory — can't close without)*
   - Receiver name + phone + GPS
   - OTP verification
   - Receiver signature
4. Rider taps **"Close Trip & Generate POD"** → data saved to cloud
5. Admin clicks **"↻ Refresh"** → POD appears in **POD Records** + **Invoice Tracker**
6. Admin downloads Customer Copy / Company Copy PDF

---

## Key Features

| Feature | Behaviour |
|---------|-----------|
| **Link Expiry** | After rider closes trip, anyone reopening the link sees "Trip Already Closed 🔒" |
| **Mandatory Images** | Rider cannot close trip without at least 1 delivery photo AND the stamped invoice photo |
| **Cross-Month Flag** | Invoice Tracker auto-flags in red if POD date is in a different month than invoice date |
| **POD in Admin** | All photos, signature, invoice copy visible in admin POD Records tab |
| **PDF Generation** | Two PDFs auto-download on trip close (Customer + Company copies) |

---

## Troubleshooting

**Rider gets "Could not Load Trip"**
→ Check JSONBin API key is correct in Settings
→ Verify the bin is set to Public in JSONBin dashboard

**Admin shows no trips after rider closes**
→ Click **"↻ Refresh"** button in top bar — data is pulled fresh from cloud

**"Update failed 401"**
→ API key in the link is wrong. Regenerate the WhatsApp link from admin

**Photos not showing in PDF**
→ Images are large — try on a desktop browser with more RAM

**JSONBin free tier limits**
→ Free: 10,000 requests/month, 100 bins, 100KB per bin
→ For scale: upgrade JSONBin plan or migrate to Supabase (ask for that version)

---

*Beyond's TMS & POD Tracker — v3.0 with JSONBin Cloud Sync*
