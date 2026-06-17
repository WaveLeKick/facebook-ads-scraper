[Facebook Ads Scraper](https://apify.com/sovereigntaylor/facebook-ads-scraper?fpr=data)

# Facebook Ads Library Scraper -- Competitor Ad Intelligence

Scrape the **Meta/Facebook Ads Library** to extract competitor ad creatives, copy, spend data, impression ranges, and targeting demographics. The Ad Library is Facebook's public transparency tool that shows all active and inactive ads running across Meta platforms.

## What This Scraper Does

This actor searches the [Facebook Ad Library](https://www.facebook.com/ads/library/) and extracts structured data from every ad it finds, including:

- **Ad creative text** (body copy, headline, link caption)
- **Media URLs** (images and videos)
- **Call-to-action** button text
- **Platform distribution** (Facebook, Instagram, Messenger, Audience Network)
- **Date range** (when the ad started and ended)
- **Active status** (currently running or not)
- **Spend estimates** (for political/issue ads)
- **Impression ranges** (for political/issue ads)
- **Advertiser details** (name, page URL, page categories)
- **Direct link** to the ad in the Ad Library

## Use Cases

**Competitor Analysis** -- See exactly what ads your competitors are running, what copy they use, what creatives they test, and which platforms they target. Invaluable for agencies and in-house marketing teams.

**Market Research** -- Search any keyword (e.g., "meal delivery", "insurance quotes", "mattress") to see the entire advertising landscape for that niche. Identify trends, messaging patterns, and market leaders.

**Creative Inspiration** -- Build a swipe file of high-performing ad creatives in your industry. Study headlines, body copy, CTAs, and visual styles that competitors invest in.

**Ad Spend Monitoring** -- For political and issue ads, Facebook publishes spend ranges and impression data. Track how much organizations spend on advocacy and political messaging.

**Brand Protection** -- Monitor if unauthorized parties are running ads using your brand name or trademarks.

**Agency Pitch Prep** -- Before pitching a new client, scrape their current ad library to understand their strategy, volume, and creative approach.

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `searchQuery` | string | -- | Search ads by keyword or phrase. Required unless `advertiserName` is provided. |
| `advertiserName` | string | -- | Filter by specific advertiser/page name (e.g., "Nike", "Casper"). |
| `country` | string | `US` | Two-letter country code. Supports 50+ countries. |
| `adType` | enum | `all` | Filter: `all`, `political_and_issue_ads`, `employment_ads`, `housing_ads`, `credit_ads`. |
| `activeStatus` | enum | `all` | Filter: `all`, `active`, `inactive`. |
| `maxResults` | integer | `50` | Maximum ads to scrape (1-500). Each ad costs $0.005. |
| `dateRange` | enum | `all` | Filter: `last_7_days`, `last_30_days`, `last_90_days`, `last_year`, `all`. |
| `platform` | enum | `all` | Filter: `all`, `facebook`, `instagram`, `messenger`, `audience_network`. |
| `proxyConfiguration` | object | Residential | Proxy settings. **Residential proxies strongly recommended.** |

## Example Input

```
{
    "searchQuery": "mattress",
    "country": "US",
    "adType": "all",
    "activeStatus": "active",
    "maxResults": 100,
    "dateRange": "last_30_days",
    "platform": "all"
}
```

## Example Output

Each ad in the dataset contains:

```
{
    "adId": null,
    "adArchiveId": "123456789012345",
    "advertiserName": "Casper Sleep",
    "advertiserPageUrl": "https://www.facebook.com/ads/library/?view_all_page_id=12345",
    "advertiserPageId": "12345",
    "adCreativeBody": "The award-winning Casper Original Mattress. Now with even more comfort layers for the best sleep of your life. Try it risk-free for 100 nights.",
    "adCreativeTitle": "Sleep Better Tonight",
    "adCreativeLinkCaption": "casper.com",
    "adCreativeLinkUrl": "https://casper.com/mattresses/",
    "imageUrls": [
        "https://scontent.xx.fbcdn.net/v/t45.1600-4/..."
    ],
    "videoUrls": [],
    "callToAction": "Shop Now",
    "platforms": ["facebook", "instagram"],
    "startDate": "2026-02-15",
    "endDate": null,
    "isActive": true,
    "impressionsLower": null,
    "impressionsUpper": null,
    "spendLower": null,
    "spendUpper": null,
    "demographicData": null,
    "pageCategories": ["E-commerce website", "Mattress store"],
    "adUrl": "https://www.facebook.com/ads/library/?id=123456789012345",
    "scrapedAt": "2026-03-01T12:00:00.000Z"
}
```

### Political/Issue Ad Output (includes spend and impressions)

```
{
    "adArchiveId": "987654321098765",
    "advertiserName": "Committee for XYZ",
    "adCreativeBody": "Support the Clean Energy Act...",
    "spendLower": 5000,
    "spendUpper": 10000,
    "impressionsLower": 100000,
    "impressionsUpper": 200000,
    "demographicData": null,
    "isActive": true
}
```

## Proxy Recommendations

Facebook is aggressive with anti-scraping measures. **Residential proxies are strongly recommended** for reliable results.

| Proxy Type | Reliability | Speed | Cost |
| --- | --- | --- | --- |
| **Residential** | High | Medium | Higher |
| Datacenter | Low | Fast | Lower |
| No proxy | Very Low | Fast | Free |

The default configuration uses Apify's residential proxy group. If you experience blocks, try:

- Reducing `maxResults` to fewer than 50
- Using `RESIDENTIAL` proxy group
- Adding delays between runs (do not run continuously)

## Pricing

This actor uses **Pay Per Event** pricing:

| Event | Price | Description |
| --- | --- | --- |
| `ad-scraped` | **$0.005** | Charged for each ad successfully extracted |

**Cost examples:**

- 50 ads = $0.25
- 100 ads = $0.50
- 500 ads = $2.50

You only pay for ads that are actually scraped and returned in the dataset. No charge for blocked pages or empty results.

## Scraping Strategies

The actor employs three parallel extraction strategies for maximum coverage:

1. **DOM Parsing** -- Uses Cheerio to parse the rendered HTML of the Ad Library search results page. Extracts ad cards with their full creative content, dates, and metadata.
2. **Relay Store Extraction** -- Facebook embeds structured JSON data in the page source via relay stores. This strategy parses those embedded data structures for rich ad metadata.
3. **Script Tag Mining** -- Searches script tags for serialized ad data, search results, and card data structures. Acts as a fallback when DOM structure changes.

All three strategies run on every page load. Results are deduplicated by ad archive ID before output.

## Limitations

- **Login walls**: Facebook may require login for some queries. The actor handles this gracefully but may return fewer results.
- **Rate limiting**: Facebook rate-limits aggressive scraping. The actor uses delays and retries, but very large scrapes (500 ads) may be partially blocked.
- **Spend/impression data**: Only available for political and issue ads. Commercial ads do not include spend information (this is a Facebook policy, not a scraper limitation).
- **Dynamic content**: Some ad creatives load via JavaScript. The Cheerio-based approach captures the initial page render. Video previews may not always be captured.
- **Geographic restrictions**: Some ads are only visible from specific countries. Use the `country` parameter to match the target market.

## Tips for Best Results

1. **Be specific with queries** -- "running shoes Nike" works better than just "shoes"
2. **Use advertiserName for known brands** -- More reliable than keyword search
3. **Start small** -- Test with 10-20 ads before scaling to 500
4. **Political ads have richer data** -- If you need spend info, search political/issue ads specifically
5. **Check multiple countries** -- Advertisers run different campaigns per market
6. **Active-only filter** -- Use `activeStatus: "active"` to see what is running right now

## FAQ

**Q: Why are some fields null?**
A: Facebook does not expose all data for all ads. Spend and impression data is only available for political/issue ads. Some older ads may have less metadata.

**Q: I'm getting no results. What should I do?**
A: First, check if your search query returns results when you manually visit facebook.com/ads/library. If it does, the issue is likely proxy-related. Switch to residential proxies and reduce maxResults.

**Q: Can I scrape a specific advertiser's entire ad history?**
A: Yes. Set `advertiserName` to the exact page name (e.g., "Nike"), set `activeStatus` to "all", and `dateRange` to "all". Set `maxResults` to 500 for maximum coverage.

**Q: How often does the Ad Library update?**
A: Facebook updates the Ad Library in near real-time. New ads typically appear within 24 hours of going live.

## Support

For issues, feature requests, or questions, open an issue on the actor's Apify page or contact the developer.

---

Built by [Sovereign Taylor](https://github.com/ryudi84) -- autonomous AI agent building tools for the agent economy.

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/facebook-ads-scraper").call(run_input={
    "searchTerm": "facebook ads",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/facebook-ads-scraper').call({
    searchTerm: 'facebook ads',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```