# Google News scraper

[![Google News scraper by cloro](https://github.com/cloro-dev/google-news-scraper/blob/main/google-news-scraper-hero-image.png)](https://cloro.dev/google-news/?utm_source=github)

[![cloro](https://img.shields.io/badge/Powered%20by-cloro-blue?style=for-the-badge)](https://cloro.dev/)

The [Google News scraper](https://cloro.dev/google-news/) by cloro enables developers to programmatically interact with Google News and automatically collect news articles with structured metadata. Instead of manual data collection, you can retrieve news articles as parsed JSON, raw HTML, or other formats for seamless integration into your workflows.

You can use cloro's Google News scraper for news monitoring, media tracking, content aggregation, and sentiment analysis. It handles dynamic content, supports real-time extraction, and eliminates the need to manage authentication, sessions, or anti-bot systems.

## How it works

The Google News scraper handles the rendering, parsing, and delivery of news articles in your requested format. You provide your search query, API credentials, and optional parameters as shown below.

### Request sample (Python)

```python
import json
import requests

# API parameters
payload = {
    'query': 'climate change',
    'country': 'US',
    'pages': 3
}

# Get a response
response = requests.post(
    'https://api.cloro.dev/v1/monitor/google/news',
    headers={'Authorization': 'Bearer YOUR_API_KEY'},
    json=payload
)

# Print response to stdout
print(response.json())

# Save response to a JSON file
with open('response.json', 'w') as file:
    json.dump(response.json(), file, indent=2)
```

### Request sample (cURL)

```bash
curl -X POST https://api.cloro.dev/v1/monitor/google/news \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "climate change",
    "country": "US",
    "pages": 3
  }'
```

### Request sample (Node.js)

```javascript
const axios = require("axios");

const payload = {
  query: "climate change",
  country: "US",
  pages: 3,
};

axios
  .post("https://api.cloro.dev/v1/monitor/google/news", payload, {
    headers: {
      Authorization: "Bearer YOUR_API_KEY",
      "Content-Type": "application/json",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Request parameters

| Parameter      | Description                                                                 | Default value |
| -------------- | --------------------------------------------------------------------------- | ------------- |
| `query`\*      | The search query for news articles (1-10,000 characters)                    | –             |
| `country`      | Optional country/region code for localized results (e.g., `US`, `GB`, `DE`) | `US`          |
| `device`       | Device type for news results (`desktop` or `mobile`)                        | `desktop`     |
| `pages`        | Number of news results pages to scrape (1-10)                               | `1`           |
| `include.html` | Include raw HTML response when set to true                                  | `false`       |

- Mandatory parameters

---

### Output samples

The Google News scraper API returns a structured JSON object containing news articles and metadata.

**Structured JSON output snippet:**

```json
{
  "success": true,
  "result": {
    "newsResults": [
      {
        "position": 1,
        "title": "Major Climate Summit Reaches Historic Agreement",
        "link": "https://example.com/climate-summit-agreement",
        "snippet": "World leaders agreed on new climate targets at the summit...",
        "source": "The Guardian",
        "date": "2 hours ago",
        "thumbnail": "https://example.com/images/climate-summit.jpg"
      },
      {
        "position": 2,
        "title": "New Climate Report Shows Urgent Need for Action",
        "link": "https://example.com/climate-report",
        "snippet": "Scientists warn that immediate action is needed to address climate change...",
        "source": "BBC News",
        "date": "5 hours ago",
        "thumbnail": "https://example.com/images/climate-report.jpg"
      }
    ],
    "html": [
      "https://storage.cloro.dev/results/a12b3c4d-5e6f-7g8h-9i0j-k1l2m3n4o5p6/page-1.html"
    ]
  }
}
```

## Advanced features

### Multi-page scraping

Scrape multiple pages of news results in a single request using the `pages` parameter (up to 10 pages). This is particularly useful for comprehensive news monitoring and analysis.

### Country-specific news

Get localized news results for different countries by specifying the `country` parameter (e.g., "US", "GB", "DE", "FR", "JP"). News content varies significantly by region.

### Device-specific results

Choose between desktop and mobile news layouts using the `device` parameter. Mobile results may show different article ordering and featured content.

### Thumbnail extraction

News articles include thumbnail images when available, perfect for building visually-rich news aggregation interfaces.

### Raw HTML access

For advanced use cases, get the complete HTML by setting `include.html` to `true`. Returns an array of HTML file URLs.

## Practical Google News scraper use cases

1. **News monitoring:** Track breaking news and trending topics in real-time.
2. **Media analysis:** Analyze media coverage across different sources and regions.
3. **Sentiment tracking:** Monitor sentiment around brands, products, or topics.
4. **Content aggregation:** Build news aggregation platforms with structured article data.
5. **Competitor intelligence:** Track competitor mentions and industry news.
6. **Research and analysis:** Gather news data for academic research or market analysis.

## Why choose cloro?

- **Simple integration:** Clean API design with comprehensive documentation and examples.
- **Reliable performance:** >99% uptime and low latencies.
- **No infrastructure hassle:** We handle rate limiting, proxies, and browser management.
- **Flexible pricing:** Low-cost subscription model with transparent pricing.
- **Developer support:** Responsive support team to help with integration and troubleshooting.

## FAQ

### Is scraping Google News allowed?

Any website is legal to be scraped as long as the information is publicly accessible.

### What makes cloro's Google News scraper unique?

cloro's Google News endpoint provides reliable access to Google News with:

- **Structured article extraction** with titles, snippets, sources, and dates
- **Thumbnail image extraction** for visual news interfaces
- **Multi-page scraping** to collect comprehensive news data
- **Built-in anti-detection** to ensure consistent results

### What's the recommended timeout for requests?

We don't recommend putting any timeout, given that our system retries automatically. We recommend setting up a retry mechanism in case of failure.

### Does the API support different countries?

Yes, you can specify country codes like `US`, `GB`, `DE`, `JP` and more to get localized news relevant to specific regions.

## Learn more

For detailed documentation, advanced features, and integration guides, visit:

- **API documentation:** [docs.cloro.dev](https://docs.cloro.dev/)
- **Google News scraper page:** [cloro.dev/google-news](https://cloro.dev/google-news/)

## Other available scrapers

- **[AI Mode](https://cloro.dev/ai-mode/)** - Extracts structured data from Google AI Mode for general knowledge queries, workflow optimization, and technical guidance.
- **[AI Overview](https://cloro.dev/ai-overview/)** - Extracts structured data from Google AI Overview for comprehensive search result analysis and AI-curated insights.
- **[ChatGPT](https://cloro.dev/chatgpt/)** - Extracts structured data from ChatGPT with advanced features including shopping cards, raw response data, and query fan-out.
- **[Copilot](https://cloro.dev/copilot/)** - Extracts structured data from Microsoft Copilot for development tools, Microsoft ecosystem research, and enterprise-focused queries.
- **[Gemini](https://cloro.dev/gemini/)** - Extracts structured data from Google Gemini for complex reasoning, content generation, and source confidence scoring.
- **[Google Search](https://cloro.dev/google-search/)** - Extracts structured data from Google Search results, including organic results, People Also Ask questions, related searches, and optional AI Overview data.
- **[Grok](https://cloro.dev/grok/)** - Extracts structured data from Grok for current events, news tracking, and real-time information gathering.
- **[Perplexity](https://cloro.dev/perplexity/)** - Extracts comprehensive structured data from Perplexity AI with real-time web sources, automatically detecting and extracting rich data objects.

## Contact us

If you have questions or need support, reach out to us at [support@cloro.dev](mailto:support@cloro.dev).

---

Built with ❤️ by the cloro team
