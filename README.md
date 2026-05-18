# Interpol Check — Landing Page

Landing page for [interpol-check.me](https://interpol-check.me) — a legal verification service by Status Law Juridiska Byrå Aktiebolag (Sweden).

## What the site does

Helps individuals and businesses verify their status in INTERPOL databases, international wanted persons lists, and law enforcement systems — and get legal help if a listing is found.

## Stack

- Pure HTML + CSS + vanilla JS — no frameworks, no build tools
- Self-hosted fonts (DM Sans, Playfair Display) — no Google Fonts, GDPR-compliant
- [Formspree](https://formspree.io) — contact form
- DNS + CDN via Cloudflare (proxy, DDoS protection, geo-detection)
- [Cloudflare Web Analytics](https://www.cloudflare.com/web-analytics/) — cookieless analytics
- [Microsoft Clarity](https://clarity.microsoft.com/) — heatmaps and session recordings
- [Google Tag Manager](https://tagmanager.google.com/) (GTM-N53MWTVH) — tag management
- [Google Ads](https://ads.google.com/) (AW-17026412757) — conversion tracking

## Structure

```
/
├── index.html         # Main landing page
├── ccf-checker.html   # CCF self-assessment quiz (6 questions, based on 60+ CCF decisions)
├── prices.json        # Regional pricing (EU / Asia)
├── fonts/             # Self-hosted woff2 font files
├── images/            # og-image.png for social sharing
├── logo.png           # Site logo
├── robots.txt
├── sitemap.xml
└── doc/               # Working files (excluded from git)
```

## Pages

### index.html — Main landing page

1. Hero — value proposition + sample verification report
2. How it works — 4-step process
3. Who needs this — target audience
4. Our cases — real CCF decisions, filtered by category
5. Pricing — transparent fixed fees, regional pricing (EU / Asia +50%)
6. Contact — secure form + messenger links (WhatsApp, Telegram, Signal, IMO)

### ccf-checker.html — CCF Self-Assessment Quiz

6-question interactive quiz that helps users assess whether their situation matches CCF Commission decisions that led to INTERPOL notice deletion. Based on 60+ verified decisions (2017–2025). Includes:
- Step-by-step questionnaire with scored answers
- Result panel with match percentage and applicable grounds
- Statistics panel: CCF decisions by ground type and year (Chart.js)
- CTA to request a consultation via the main site contact form

## Regional pricing

Prices are stored in `prices.json` and applied via JS on page load.
Region is detected through Cloudflare `/cdn-cgi/trace` (no external API needed).
- **EU** — base prices
- **Asia** — +50% (covers East, Southeast, South and Central Asia)
- All other regions — EU prices by default

## Conversion tracking

Messenger clicks fire individual GTM custom events:
- `click_whatsapp`, `click_telegram`, `click_signal`, `click_imo`

Form submission fires a Google Ads conversion: `AW-17026412757/2roxCJDRuZscENXh6bY_`

## Form submission pipeline

On successful form submit, four things happen in parallel:
1. **Formspree** — receives and stores the submission, sends email notification
2. **Planfix** — creates a task via REST API (`/rest/task`) with name, description, project (id: 804) and counterparty (id: 306)
3. **Google Ads** — fires conversion event
4. **GTM dataLayer** — pushes `form_submitted` event

## Form auto-fill on page load

Using Cloudflare `/cdn-cgi/trace`, the page detects the visitor's country and:
- Pre-selects the country in the contact form dropdown
- Sets the phone prefix placeholder
- Updates the hidden form subject field with the country code

## Contacts

**Status Law Juridiska Byrå Aktiebolag**  
Bygdegatan 313, Linköping, Sweden  
[status.law](https://status.law) · info@status.law
