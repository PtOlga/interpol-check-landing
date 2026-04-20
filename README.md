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
- [Ahrefs Web Analytics](https://ahrefs.com/web-analytics/) — SEO-oriented analytics
- [Microsoft Clarity](https://clarity.microsoft.com/) — heatmaps and session recordings
- [Google Tag Manager](https://tagmanager.google.com/) (GTM-N53MWTVH) — tag management
- [Google Ads](https://ads.google.com/) (AW-17026412757) — conversion tracking

## Structure

```
/
├── index.html        # Main landing page
├── prices.json       # Regional pricing (EU / Asia)
├── fonts/            # Self-hosted woff2 font files
├── images/           # og-image.png for social sharing
├── logo.png          # Site logo
├── robots.txt
├── sitemap.xml
└── doc/              # Working files (excluded from git)
```

## Sections

1. Hero — value proposition + sample verification report
2. How it works — 4-step process
3. Who needs this — target audience
4. Our cases — real CCF decisions, filtered by category
5. Pricing — transparent fixed fees, regional pricing (EU / Asia +50%)
6. Contact — secure form + messenger links (WhatsApp, Telegram, Signal, IMO)

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

## Contacts

**Status Law Juridiska Byrå Aktiebolag**  
Bygdegatan 313, Linköping, Sweden  
[status.law](https://status.law) · info@status.law
