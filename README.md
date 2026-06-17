[Facebook Ads Scraper](https://apify.com/good-apis/facebook-ads-scraper?fpr=data)

# Facebook Ads Scraper

Scrape Meta's Ad Library for complete ad data — creative, audience reach, page intelligence, spend, and more.

## Features

- **Search** — Find ads by page slug or keyword across any country
- **Complete ad data** — Every search result includes full details: creative, images, videos, audience reach, spend, page metadata
- **47-field output** — The richest Facebook Ads data available on Apify
- **Page intelligence** — 32-field page profiles: about text, verification status, entity type, category, cover photo, and more
- **Audience reach** — Total reach, demographic breakdown by age/gender/region (where available)
- **Full ad creative** — body, title, images, videos, carousel cards, CTA, display format
- **Spend & impressions** — with upper/lower bounds
- **Publisher platforms** — Facebook, Instagram, Messenger, Audience Network

## Pricing

**$0.75 per 1,000 ads** (Pay Per Event) — you only pay for ads delivered.

## Actions

### `search` — Search Ad Library

Search for ads by Facebook page slug or keyword. Each result includes complete ad data with creative, spend, audience reach, and page intelligence.

**Required input:**

- `slug` — Page slug or search keyword (e.g. "hubspot", "medvi", "weight loss")

**Optional input:**

- `country` — Country code (default: "US"). Examples: US, FR, GB, DE
- `max_ads` — Maximum number of ads to return (default: 150, max: 15000). Pagination stops as soon as this is reached, so you only pay for what you ask for.
- `active_only` — Only return active ads (default: false)

### `detail` — Single Ad Lookup

Get complete data for a single ad by archive ID.

**Required input:**

- `ad_archive_id` — The ad archive ID (from search results)
- `page_id` — The Facebook page ID (from search results)

**Optional input:**

- `country` — Country code (default: "US")

## Example Input

### Search

```
{
    "action": "search",
    "slug": "hubspot",
    "country": "US",
    "max_ads": 100,
    "active_only": true
}
```

### Detail

```
{
    "action": "detail",
    "ad_archive_id": "1617980282547010",
    "page_id": "108624140548097",
    "country": "US"
}
```

## Example Output

### Search result (one ad)

```
{
    "library_id": "1617980282547010",
    "page_id": "108624140548097",
    "page_name": "HubSpot",
    "page_likes": 1250000,
    "page_category": "Software",
    "page_about": "HubSpot is a CRM platform with all the software...",
    "page_verification": "blue_verified",
    "page_cover_photo": "https://...",
    "entity_type": "PERSON_PROFILE",
    "is_political_page": false,
    "ad_body": "Grow better with HubSpot...",
    "ad_title": "Free CRM Software",
    "cta_text": "Learn more",
    "images": ["https://..."],
    "cards": [{"body": "...", "title": "..."}],
    "start_date": "2026-02-06",
    "is_active": true,
    "publisher_platforms": ["facebook", "instagram"],
    "spend": {"lower_bound": "100", "upper_bound": "499", "currency": "USD"},
    "impressions": {"lower_bound": "10000", "upper_bound": "14999"},
    "reach_estimate": 756,
    "targeted_countries": ["US"],
    "collation_count": 4,
    "display_format": "DCO"
}
```

## Notes

- Use `max_ads` to cap how many ads are returned (and how much you pay).
- Each ad in search results comes with full details.
- Requests may take 30-60 seconds.
- Audience reach data availability depends on ad type and region.
- Some ads may not have spend/impressions data.