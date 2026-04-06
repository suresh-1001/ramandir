# Shree Ram Mandir EPA – Hugo Website

Hugo static site for rammandirepa.org, hosted on GitHub Pages.

## Quick Setup

### 1. Prerequisites
```bash
# Install Hugo (extended)
brew install hugo        # macOS
winget install Hugo.Hugo.Extended  # Windows
```

### 2. Clone and run locally
```bash
git clone https://github.com/YOUR_ORG/rammandirepa.git
cd rammandirepa
hugo server -D
# Open http://localhost:1313
```

### 3. Configure before going live

Edit `hugo.toml` and update these values:

| Key | What to set |
|-----|-------------|
| `baseURL` | `https://www.rammandirepa.org/` |
| `googleCalID` | Google Calendar ID (see below) |
| `paypalDonateURL` | New PayPal.me donate link |
| `web3formsKey` | Web3Forms access key from web3forms.com |

---

## Google Calendar Setup

This is how the festival calendar stays automatically updated:

1. Go to [calendar.google.com](https://calendar.google.com)
2. Create a new calendar: **"Shree Ram Mandir EPA Festivals"**
3. Add all festival dates from `data/festivals.yaml` as events
4. Make the calendar **public**: Settings → Access permissions → ✅ Make available to public
5. Get the Calendar ID: Settings → scroll to "Integrate calendar" → copy the Calendar ID (looks like `abc123@group.calendar.google.com`)
6. Paste it into `hugo.toml` as `googleCalID`

**To add recurring buttons (iCal / Google Calendar subscribe):**  
The calendar page already generates subscribe links automatically once the ID is set.

---

## PayPal Donation Setup

The old PayPal buttons are broken. To fix:

1. Log in to the mandir's PayPal Business account
2. Go to **Pay & Get Paid → Donation buttons**
3. Create a new Donate button → copy the hosted button ID
4. Update `hugo.toml` → `paypalDonateURL`
5. For recurring tiers, create PayPal Subscription buttons and update `data/donate_tiers.yaml`

---

## Web3Forms Contact Form

1. Go to [web3forms.com](https://web3forms.com)
2. Enter `epamandir@gmail.com` → get your free access key
3. Paste the key into `hugo.toml` → `web3formsKey`
4. Test the form — submissions arrive directly to Gmail

---

## Updating Festival Dates Annually

Two steps each January:

**Step 1 — Update the static reference table:**
Edit `data/festivals.yaml` with dates from [drikpanchang.com](https://www.drikpanchang.com) for the new year.

**Step 2 — Update Google Calendar:**
Add/edit events in the mandir Google Calendar. The website embed updates automatically — no rebuild needed.

---

## Adding Photos to Gallery

Drop images into:
```
static/images/gallery/event-name/photo1.jpg
static/images/gallery/event-name/photo2.jpg
```

Then add `<div class="gallery-item">` entries to `layouts/_default/gallery.html`.

---

## Deploying

Push to `main` branch — GitHub Actions builds and deploys automatically.

```bash
git add .
git commit -m "Update festival calendar 2026"
git push origin main
```

**GitHub Pages setup (one-time):**
1. Repo Settings → Pages → Source: **GitHub Actions**
2. The `.github/workflows/hugo.yml` handles the rest

**Cloudflare DNS:**
```
CNAME  www   YOUR_ORG.github.io
```
Add `static/CNAME` file with content: `www.rammandirepa.org`

---

## Site Structure

```
content/
├── _index.md           # Homepage
├── about.md            # About + mission + construction project
├── calendar.md         # Festival calendar (Google Cal embed + static table)
├── contact.md          # Web3Forms contact form
├── donate.md           # PayPal donate page
├── thank-you.md        # Form submission confirmation
├── events/             # Event posts (Faag Samelan, Hanuman Jayanti, etc.)
├── prayers/            # Aarti and prayer PDFs
└── gallery/            # Photo gallery

data/
├── festivals.yaml      # Static festival reference table (update annually)
└── donate_tiers.yaml   # PayPal monthly subscription tiers

static/
├── css/main.css        # All styles
├── pdfs/               # LaxmiAarti.pdf and other prayer PDFs
└── images/             # Site images and gallery photos
```

---

*Jai Sia Ram! — Shree Ram Mandir East Palo Alto*
