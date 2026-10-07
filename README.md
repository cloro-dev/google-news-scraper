# Google News Scraper

[![Google News Scraper by cloro](https://github.com/cloro-dev/google-news-scraper/blob/main/google-news-scraper-hero-image.png)](https://cloro.dev/google-news/?utm_source=github)

[![cloro](https://img.shields.io/badge/Powered%20by-cloro-blue?style=for-the-badge)](https://cloro.dev/)

The [Google News scraper](https://cloro.dev/google-news/?utm_source=github) by cloro returns Google News results as structured JSON: article titles, snippets, sources, publication dates and thumbnails.

## How do you scrape Google News?

1. Get an API key at [cloro.dev](https://cloro.dev/?utm_source=github&utm_medium=readme).
2. POST a query to `https://api.cloro.dev/v1/monitor/google/news`.
3. Read the parsed fields from the JSON response.

News is the surface where freshness beats everything else, so the endpoint is built for repeated polling of the same query rather than deep one-off pulls. Use `pages` to widen coverage and `country` to change the edition.

### Request sample (Python)

```python
import requests

payload = {
    'query': 'AI search regulation',
    'country': 'US',
    'pages': 1,
}

response = requests.post(
    'https://api.cloro.dev/v1/monitor/google/news',
    headers={'Authorization': 'Bearer YOUR_API_KEY'},
    json=payload,
)

print(response.json())
```

### Request sample (cURL)

```bash
curl -X POST https://api.cloro.dev/v1/monitor/google/news \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "AI search regulation", "country": "US"}'
```

Node.js and async/webhook examples are in the [endpoint documentation](https://cloro.dev/docs/api-reference/endpoint/monitor-google-news).

### Request parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `query`\* | The news search query | – |
| `country`\* | Country code, which selects the Google News edition. Required unless you send `gl` | – |
| `device` | `desktop`, `mobile`, `ios` or `android` | `desktop` |
| `pages` | Number of result pages to return | `1` |
| `include.html` | Return URLs to the full HTML, one per page (expire after 24h) | `false` |

\* Required

## What data does the Google News scraper return?

```json
{
  "success": true,
  "result": {
    "newsResults": [
      {
        "position": 1,
        "title": "Regulators open inquiry into AI search results",
        "link": "https://example.com/news/ai-search-inquiry",
        "source": "Example Times",
        "date": "2 hours ago",
        "snippet": "The inquiry will examine how AI answers attribute sources...",
        "thumbnail": "https://example.com/thumb.jpg"
      }
    ]
  }
}
```

1. **`newsResults`** — position, title, link, source, date, snippet and thumbnail per article.
2. **`html`** — an array of URLs to the full rendered pages, one per page, when `include.html` is set, expiring after 24 hours.

The structure is deliberately flat. News has no AI Overview, no shopping block and no local pack, so there is nothing else to parse.

Full field-level schemas are in the [endpoint reference](https://cloro.dev/docs/api-reference/endpoint/monitor-google-news).

## Use cases

- **Media monitoring** — track coverage of a brand, product or competitor by query.
- **Crisis detection** — poll a branded query on a short interval and alert on new sources.
- **Source-mix analysis** — which publications Google News surfaces for a topic, and how that changes.
- **Content research** — what has already been written before you commission a piece.

## FAQ

### How fresh are the results?

As fresh as Google News itself. The `date` field is returned as Google renders it, usually relative for recent items.

### Can I get a specific country edition?

Yes, via `country`. Editions differ in both source mix and ordering, so a US and a GB pull on the same query are genuinely different result sets.

### Is there a date filter?

Not on this endpoint. Filter on the returned `date` field, or narrow the query.

### Is scraping Google News allowed?

cloro returns publicly visible results. Article text itself stays with the publisher; use the snippets and links rather than reproducing full articles.

## Learn more

- **Endpoint reference:** [cloro.dev/docs](https://cloro.dev/docs/api-reference/endpoint/monitor-google-news)
- **Product page:** [cloro.dev/google-news](https://cloro.dev/google-news/)

## Other cloro scrapers

[AI Mode](https://cloro.dev/ai-mode/) · [AI Overview](https://cloro.dev/ai-overview/) · [ChatGPT](https://cloro.dev/chatgpt/) · [Copilot](https://cloro.dev/copilot/) · [Gemini](https://cloro.dev/gemini/) · [Google Search](https://cloro.dev/google-search/) · [Grok](https://cloro.dev/grok/) · [Perplexity](https://cloro.dev/perplexity/)

## Contact us

Questions or support: [ask the docs AI assistant](https://cloro.dev/docs/?assistant).
