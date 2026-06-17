[Facebook Ads Scraper](https://apify.com/alizarin_refrigerator-owner/facebook-ads-scraper?fpr=data)

# Facebook Ad Library Scraper - Competitor Ad Intelligence

Discover competitor Facebook ads by scraping Meta's Ad Library. Find active and inactive ads, see creatives, and analyze messaging. No per-campaign fees.

---

## Quick Start

### Test with Demo Mode (free, no API key needed)

```
{
  "demoMode": true
}
```

### Run with real data

```
{
  "demoMode": false,
  "countryCode": "US",
  "maxItems": 50,
  "adActiveStatus": "ALL",
  "webhookPlatform": "custom"
}
```

---

## Input Parameters

| Parameter | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| `pageIds` | array | - | No | List of Facebook Page IDs to scrape ads from |
| `searchTerm` | string | - | No | Search term to find ads (alternative to pageIds) |
| `countryCode` | string | `"US"` | No | Country to filter ads (ISO 2-letter code) |
| `maxItems` | integer | `50` | No | Maximum number of ads to scrape per page |
| `adActiveStatus` | string | `"ALL"` | No | Filter by ad status |
| `demoMode` | boolean | `true` | No | Run with sample data to test without real scraping. Returns realistic sample output instantly. Set to false and provide pageIds or searchTerm for real scraping. |
| `webhookUrl` | string | - | No | URL to POST results when scraping completes (Zapier, Make, n8n, custom endpoint) |
| `webhookPlatform` | string | `"custom"` | No | Platform type for webhook formatting |
| `webhookHeaders` | object | - | No | Custom HTTP headers to send with webhook (JSON object) |

---

## Pricing

This actor uses **pay-per-event** billing:

| Event | Description | Price |
| --- | --- | --- |
| Ad Scraped | Each Facebook ad scraped from Ad Library | $0.04 |

**Demo mode is free** -- no charges for sample data.

---

## Troubleshooting

### "API error 429" or "Rate limit"

Too many requests. Wait a minute and try again, or reduce the number of items per run.

### No results or empty dataset

Check the run log for error messages. Common causes:

- Invalid input format (check the examples above)
- The target data doesn't exist or is too small to track

### How do I test without an API key?

Enable **Demo Mode** in the input. This returns realistic sample data so you can verify the output format works for your workflow.

---

**Built by John Rippy | [Actor Arsenal](https://actorarsenal.com)**