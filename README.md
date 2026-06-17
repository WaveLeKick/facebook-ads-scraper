[Facebook Ads Scraper](https://apify.com/dltik/facebook-ads-scraper?fpr=data)

**Facebook Ads Library Scraper** lets you **search and extract Facebook & Instagram ads** from the official Meta Ad Library — without any API token or developer account. Enter a keyword and country, get ad copy, page info, platforms, dates, creative URLs, and auto-enrichment (CTA detection, ad categorization, running duration).

> **No API token needed. No proxy needed.** Just enter a keyword and click Start. The fastest way to spy on competitor ads.

 

> ⭐ **Found this useful?** Click the **Bookmark** button at the top of [this page](https://apify.com/dltik/facebook-ads-scraper) — it helps the scraper stay visible to others who need it. Takes 1 click. No signup beyond your existing Apify account.

---

## What can Facebook Ads Library Scraper do?

- 🔍 **Search ads by keyword** — find all ads containing "fitness", "dropshipping", "skincare", etc.
- 📄 **Search ads by page** — get all ads from a specific Facebook page
- 🌍 **Filter by country** — target ads shown in any country or worldwide
- 📊 **Active/inactive filter** — see only running ads or recently stopped ones
- 🤖 **Auto-enrichment** — CTA detection, ad category (ecommerce/lead gen/app install), running duration, hashtags, emoji count
- 📱 **Platform detection** — which platforms the ad runs on (Facebook, Instagram, Messenger)
- ⚡ **No API token required** — works out of the box, zero configuration

---

## What data can you extract from Facebook Ads?

| Field | Description |
| --- | --- |
| `page_name` | Advertiser page name |
| `ad_text` | Full ad copy / creative body |
| `start_date` | When the ad started running |
| `end_date` | When the ad stopped (null if still active) |
| `is_active` | Whether the ad is currently running |
| `platforms` | Facebook, Instagram, Messenger, Audience Network |
| `ad_snapshot_url` | Direct link to view the ad creative |
| `ad_id` | Meta Ad Library ID |
| `media_type` | Image, video, or carousel |
| `ad_category` | Auto-detected: ecommerce, lead_gen, app_install, video, brand_awareness |
| `detected_ctas` | Call-to-action phrases found (Shop Now, Sign Up, Learn More...) |
| `duration_days` | How many days the ad has been running |
| `hashtags` | Hashtags used in the ad copy |
| `word_count` | Number of words in the ad text |

---

## How to search Facebook ads

1. **[Create a free Apify account](https://apify.com/sign-up)** — no credit card required
2. **Open [Facebook Ads Library Scraper](https://apify.com/dltik/facebook-ads-scraper)** in Apify Store
3. **Enter a keyword** (e.g. `fitness`) and **select a country** (e.g. `FR`)
4. **Choose filters** — active/inactive, max results
5. **Click Start** — ads start appearing in seconds
6. **Download your results** in JSON, CSV, or Excel

---

## How much does it cost to scrape Facebook ads?

**$0.001 per ad extracted** ($1 per 1,000 ads).

| Run size | Ads | Apify cost | Time |
| --- | --- | --- | --- |
| Quick test (10 ads) | 10 | ~$0.01 | ~30s |
| Small batch (50 ads) | 50 | ~$0.05 | ~1min |
| Standard (200 ads) | 200 | ~$0.20 | ~3min |
| Large (500 ads) | 500 | ~$0.50 | ~8min |

---

## Input

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `searchTerms` | string | ❌ | — | Keywords to search (e.g. `fitness`) |
| `pageId` | string | ❌ | — | Facebook Page ID to get all its ads |
| `country` | string | ❌ | `ALL` | Country code (FR, US, GB, DE...) or ALL |
| `activeStatus` | string | ❌ | `all` | `all`, `active`, or `inactive` |
| `maxResults` | integer | ❌ | `50` | Max ads to return (1-500) |
| `enrichAds` | boolean | ❌ | `true` | Add CTA detection, category, duration |

> Provide either `searchTerms` or `pageId` (or both).

---

## Output example

```
{
  "ad_id": "1234567890",
  "page_name": "FitnessBrand",
  "ad_text": "Get 50% off our best-selling protein powder! Limited time offer. Shop now at fitnessbrand.com #fitness #protein",
  "start_date": "Mar 16, 2026",
  "end_date": null,
  "is_active": true,
  "platforms": ["facebook", "instagram"],
  "ad_snapshot_url": "https://www.facebook.com/ads/library/?id=1234567890",
  "media_type": "image",
  "ad_category": "ecommerce",
  "detected_ctas": ["shop now"],
  "duration_days": 13,
  "hashtags": ["#fitness", "#protein"],
  "emoji_count": 0,
  "word_count": 18
}
```

---

## Use cases

- **Competitor ad research** — see exactly what ads your competitors are running right now
- **Dropshipping product research** — find winning products by searching ad keywords
- **Agency reporting** — track client competitors' ad strategies over time
- **Creative inspiration** — browse thousands of ad copies in your niche
- **Market research** — understand what's being advertised in any country and industry

---

## Use Facebook Ads Scraper via API

**Python:**

```
import requests

run = requests.post(
    "https://api.apify.com/v2/acts/dltik~facebook-ads-scraper/runs",
    headers={"Authorization": "Bearer YOUR_APIFY_TOKEN"},
    json={
        "searchTerms": "fitness",
        "country": "FR",
        "maxResults": 100,
        "enrichAds": True
    }
).json()

print(f"Run started: {run['data']['id']}")
```

**curl:**

```
curl -X POST "https://api.apify.com/v2/acts/dltik~facebook-ads-scraper/runs" \
  -H "Authorization: Bearer YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"searchTerms": "fitness", "country": "FR", "maxResults": 50}'
```

---

## FAQ

**Do I need a Facebook account or API token?**

No. The Meta Ad Library is a public transparency tool. This actor scrapes it directly — no login, no API token, no developer account needed.

**What's the difference between this and the Meta Ad Library API?**

The official API requires a developer account, app review, and access token management. This actor gives you the same data with zero setup. Just enter a keyword and click Start.

**Can I search ads from a specific competitor?**

Yes. Use the `pageId` parameter with your competitor's Facebook Page ID. You can find the page ID in the page's URL or About section.

**Why do some ads have no text?**

Some ads are image-only or video-only without body text. The `ad_text` field will be empty but you'll still get the page name, dates, platforms, and snapshot URL.

**How often does the Ad Library update?**

Meta updates the Ad Library in near-real-time. New ads appear within hours of going live. Stopped ads are marked inactive.

**I need help or a custom solution.**

Open an issue on the [Issues tab](https://apify.com/dltik/facebook-ads-scraper/issues) or contact us through Apify.

---

## Connect with Make, Zapier & n8n

This actor integrates with any automation platform via the Apify API.

### Make (Integromat)

1. Add an **Apify module** in your Make scenario
2. Select **Run Actor** and choose this actor
3. Configure the input (paste your JSON)
4. Add a **Get Dataset Items** module to retrieve results
5. Connect to Google Sheets, HubSpot, Slack, or any other app

### Zapier

1. Use the **Apify integration** on Zapier
2. Set trigger: **Actor Run Finished**
3. Action: **Get Dataset Items**
4. Send results to your CRM, email tool, or spreadsheet

### n8n

1. Add an **HTTP Request** node to call the Apify API
2. POST to `https://api.apify.com/v2/acts/dltik~facebook-ads-scraper/runs`
3. Wait for completion, then fetch dataset items
4. Route results to any n8n node

### Webhooks

Set up a webhook to get notified when a run finishes:

```
run = client.actor("dltik/facebook-ads-scraper").call(
    run_input={...},
    webhooks=[{
        "eventTypes": ["ACTOR.RUN.SUCCEEDED"],
        "requestUrl": "https://your-webhook-url.com"
    }]
)
```

---

---

⭐ **Found this Facebook Ads Library Scraper useful? Bookmark it** — Apify ranks actors by bookmarks, so it's the strongest single signal for Store visibility. One click = directly helps this actor stay surfaced.

## Other scrapers by dltik

| Actor | What it does | Price |
| --- | --- | --- |
| [Google Maps Email Extractor](https://apify.com/dltik/google-maps-email-extractor) | Extract emails, phones, WhatsApp from Google Maps businesses | $25/1K |
| [TikTok Scraper](https://apify.com/dltik/tiktok-scraper) | Scrape profiles, videos, hashtags, search, trending | $1/1K |
| [TikTok Video Downloader](https://apify.com/dltik/tiktok-video-downloader) | Download TikTok videos without watermark | $5/1K |
| [Reddit Scraper](https://apify.com/dltik/reddit-scraper) | Scrape posts, comments, profiles with sentiment analysis | $2/1K |
| [Trustpilot Scraper](https://apify.com/dltik/trustpilot-scraper) | Scrape reviews, ratings, company profiles with sentiment | $0.50/1K |
| [HackerNews MCP Server](https://apify.com/dltik/mcp-server-hackernews) | HN search for AI agents — tech audience research | $5/1K |