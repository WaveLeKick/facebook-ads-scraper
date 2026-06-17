[Facebook Ads Scraper](https://apify.com/sourabhbgp/facebook-ads-scraper?fpr=data)

# Facebook Ads Library Scraper | Meta Ad Library + Instagram Data | 57 Fields | No Login

Scrape the **Meta Ad Library** (Facebook Ads Library) at scale with **57 fields per ad** — ad copy, images, videos, CTAs, run dates, publisher platforms, Instagram followers, page verification, EU transparency flags, AI-generated media detection, and more. **No Facebook account, no cookies, no login required.** Uses Meta's internal GraphQL API directly for fast, reliable HTTP-based extraction.

## Why Use This Scraper?

- **No login, no cookies, no Facebook account needed** — fully anonymous access
- **57 fields per ad** — the most comprehensive Meta Ad Library scraper on Apify
- **Clean flat output** — no deeply nested JSON, every field at top level
- **URL input mode** — paste any Meta Ad Library URL, filters parsed automatically
- **Built-in residential proxy** — anti-blocking handled automatically
- **Instagram data included** — IG followers, username, verification status via `enrichDetails`
- **AI-generated content flag** — detect digitally-created/AI media in ads (`containsDigitalCreatedMedia`)
- **Competitor intelligence ready** — scrape thousands of ads per run, export to JSON/CSV/Excel

## What Data You Get (All 57 Fields)

### Core ad fields

`adArchiveId`, `adId`, `collationId`, `isActive`, `startDate`, `endDate`, `totalActiveTime`, `publisherPlatforms` (Facebook, Instagram, Messenger, Threads, WhatsApp), `targetedOrReachedCountries`

### Ad creative

`adCopy`, `title`, `caption`, `linkDescription`, `linkUrl`, `ctaText`, `ctaType`, `displayFormat` (IMAGE/VIDEO/DCO/CAROUSEL/DPA), `byline`, `disclaimerLabel`

### Media

`images` (original + resized URLs), `videos` (HD, SD, preview), `cards` (full carousel data with per-card body, title, CTA, images, videos, watermarked variants)

### Advertiser page

`pageId`, `pageName`, `pageUrl`, `pageLikes`, `pageCategories`, `pageProfilePictureUrl`

### Enrich data (when `enrichDetails: true`)

`pageAlias`, `pageCategory`, `pageAbout`, `pageCoverPhotoUrl`, `pageVerification` (BLUE_VERIFIED/NOT_VERIFIED), `entityType` (BUSINESS/PERSON_PROFILE/BRAND), `igUsername`, `igFollowers`, `igVerification`, `isProfilePage`, `isPoliticalPage`

### Transparency & regulation

`categories`, `gatedType`, `hideDataStatus`, `isAaaEligible` (EU transparency), `hasUserReported`, `reportCount`, `menuItems`, `stateMediaRunLabel`, `containsDigitalCreatedMedia`, `containsSensitiveContent`, `regionalRegulationData` (finserv, anti-scam flags)

### Impressions & spend (political ads)

`impressionsText`, `impressionsIndex`, `reachEstimate`, `currency`, `spend`

### Meta

`collationCount`, `scrapedAt`

## Input Options

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `mode` | select | `search` | `search` (by keyword) or `advertiser` (by page) |
| `query` | string | `marketing` | Keyword to search for |
| `advertiserUrls` | list | — | Facebook Page URLs or numeric Page IDs |
| `urls` | list | — | Full Ads Library URLs (all filters parsed automatically) |
| `country` | string | `US` | ISO 2-letter country code |
| `countries` | list | — | Multiple countries (overrides single `country`) |
| `activeStatus` | select | `active` | `active`, `inactive`, or `all` |
| `adType` | select | `all` | `all` or `political_and_issue_ads` |
| `mediaType` | select | `all` | `all`, `image`, or `video` |
| `platforms` | list | — | FACEBOOK, INSTAGRAM, MESSENGER, THREADS, WHATSAPP |
| `languages` | list | — | Content language codes (e.g. `en`, `es`, `fr`) |
| `startDate` | date | — | Only ads active on or after this date |
| `endDate` | date | — | Only ads started on or before this date |
| `maxResults` | integer | `100` | Max ads (0 = unlimited) |
| `enrichDetails` | boolean | `false` | Fetch Instagram followers + page verification per ad |
| `proxyConfiguration` | object | Apify Residential | Required — Meta blocks datacenter IPs. BYO proxy supported. |

## How to Use — 3 Ways

### 1. Paste an Ads Library URL (easiest)

Go to [facebook.com/ads/library](https://www.facebook.com/ads/library), apply filters, copy the URL, paste into `urls`:

```
{
    "urls": [
        "https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=US&q=shopify&media_type=video"
    ],
    "maxResults": 200
}
```

### 2. Keyword search

```
{
    "mode": "search",
    "query": "dropshipping",
    "country": "US",
    "activeStatus": "active",
    "platforms": ["INSTAGRAM"],
    "maxResults": 500
}
```

### 3. Advertiser mode

Scrape all ads run by specific pages:

```
{
    "mode": "advertiser",
    "advertiserUrls": [
        "15087023444",
        "https://www.facebook.com/shopify"
    ],
    "activeStatus": "all",
    "maxResults": 1000,
    "enrichDetails": true
}
```

## Example Output (Real Ad)

```
{
    "adArchiveId": "820793561047630",
    "pageId": "15087023444",
    "pageName": "Nike",
    "pageUrl": "https://www.facebook.com/nike/",
    "pageAlias": "nike",
    "pageLikes": 39200000,
    "pageCategory": "Sportswear",
    "pageAbout": "#givesyouwings",
    "pageProfilePictureUrl": "https://scontent.fbcdn.net/...",
    "pageCoverPhotoUrl": "https://scontent.fbcdn.net/...",
    "pageVerification": "BLUE_VERIFIED",
    "entityType": "BUSINESS",
    "igUsername": "nike",
    "igFollowers": 306000000,
    "igVerification": true,
    "isProfilePage": false,
    "isPoliticalPage": false,
    "isActive": true,
    "startDate": "2026-01-19T07:00:00.000Z",
    "endDate": null,
    "totalActiveTime": 7862400,
    "publisherPlatforms": ["FACEBOOK", "INSTAGRAM"],
    "adCopy": "Ball's in your court. Get the gear that never misses.",
    "title": "Nike Air Max",
    "caption": "nike.com",
    "linkUrl": "https://www.nike.com/...",
    "ctaText": "Shop Now",
    "ctaType": "SHOP_NOW",
    "displayFormat": "IMAGE",
    "images": [{ "originalUrl": "...", "resizedUrl": "..." }],
    "videos": [],
    "cards": [],
    "collationCount": 3,
    "gatedType": "ELIGIBLE",
    "isAaaEligible": false,
    "containsDigitalCreatedMedia": false,
    "containsSensitiveContent": false,
    "scrapedAt": "2026-04-17T10:00:00.000Z"
}
```

## Pricing

**$2 per 1,000 ads** today ($0.002/ad). Dropping to **$0.99/1K on 2026-05-02** (Apify requires 14-day notice for price decreases).

Apify residential proxy (required) adds approximately $0.025/1K in platform fees (measured on real runs: 3.2 KB/ad × $8/GB = $0.025/1K). Users may bring their own proxy via `proxyConfiguration.proxyUrls` to skip this cost.

### Price comparison vs competitors

| Scraper | Their price | Requires |
| --- | --- | --- |
| `apify/facebook-ads-scraper` | $3.40 – $5.80/1K | Apify proxy (bundled) |
| `easyapi/facebook-ads-library-scraper` | $2.99/1K | — |
| `dz_omar/facebook-ads-scraper-pro` | $10/1K FREE → $0.40 GOLD | bundled |
| `curious_coder/facebook-ads-library-scraper` | $0.75/1K | **user must provide proxy** ($3–10+/GB extra) |
| **This scraper** | **$0.99/1K (from May 2)** | Apify residential proxy (+~$0.025/1K) |

## Use Cases

- **Competitor ad intelligence** — monitor what ads competitors are running, their copy, creatives, CTAs, and campaign longevity
- **Market research** — analyze advertising trends for any keyword, niche, or industry across 40+ countries
- **Lead generation** — find active advertisers in specific niches, filter by platform or country
- **Ad creative inspiration** — extract successful ad formats, headlines, CTAs, and copy from top brands
- **Brand monitoring** — track how brands advertise across Facebook, Instagram, Messenger, and Threads
- **Political ad tracking** — monitor political and issue ads with spend and impression data
- **AI content detection** — flag ads that use AI-generated imagery (`containsDigitalCreatedMedia`)
- **EU transparency research** — identify AAA-eligible ads and access regional regulation data
- **Influencer research** — use `enrichDetails` to get Instagram follower counts and verification status

## Technical Details

- **Architecture**: HTTP-only, no browser automation. Uses Meta's internal GraphQL API (`AdLibrarySearchPaginationQuery` and `AdLibraryV3AdDetailsQuery`).
- **Authentication**: Anonymous `rd_challenge` bypass — no Facebook account required.
- **Session caching**: Auth session cached for up to 20 hours across runs (24h cookie lifetime).
- **Proxy rotation**: Auto-rotates residential IPs on rate-limiting (Meta rate-limits Apify datacenter IPs).
- **Pagination**: Cursor-based, 30 ads per API call, unlimited depth.
- **Success rate target**: 98%+ on Apify platform with residential proxy.

## FAQ

**Q: Do I need a Facebook account?**
No. The actor uses anonymous access — the Meta Ad Library is a public transparency tool.

**Q: Why does it need a proxy?**
Meta rate-limits Apify's shared datacenter IPs within seconds. Residential proxy is required for reliable operation. You can bring your own proxy via `proxyConfiguration.proxyUrls`.

**Q: What's the difference between `search` and `advertiser` mode?**
`search` finds ads matching a keyword across all advertisers. `advertiser` gets all ads from specific Facebook pages (more precise for competitor tracking).

**Q: Can I paste any Meta Ad Library URL?**
Yes. Go to facebook.com/ads/library, apply filters, copy the URL, paste into `urls`. All filters (keyword, country, platforms, languages, date range) are extracted automatically.

**Q: What does `enrichDetails: true` do?**
Makes one additional API call per ad to fetch Instagram follower count, page verification status, entity type, page category, "About" text, and Instagram username. Slower but provides the richest advertiser profile.

**Q: Does it work for political ads?**
Yes. Set `adType: "political_and_issue_ads"`. Political ads include `spend`, `impressions`, and `reachEstimate` data.