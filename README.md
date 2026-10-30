<p align="center">
  <a href="https://www.piloterr.com"><img src="images/banner.png" alt="Ocean.io Scraper API by Piloterr – scrape Ocean.io data as JSON" width="100%"></a>
</p>

# Ocean.io Scraper API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/Piloterr-Get%20a%20free%20API%20key-111827)](https://app.piloterr.com) [![API docs](https://img.shields.io/badge/Docs-OpenAPI-0EA5E9)](https://app.piloterr.com/openapi) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **Piloterr Ocean.io Scraper API** lets you extract public data from Ocean.io as **clean, structured JSON** — no proxies, headless browsers or HTML parsing to maintain. Endpoints available in production:

- **Oceanio Search API** — Search the Ocean.io B2B database by domain to find similar companies, retrieve contact details, employee profiles, and social network links.

Use it for lead generation, CRM enrichment, market mapping, investment research or job market analytics.

| Endpoint | Path | Credits | What you get |
|---|---|---|---|
| [Oceanio Search API](#oceanio-search-api) | `/v2/oceanio/search` | 1 | Search the Ocean.io B2B database by domain to find similar companies, retrieve contact details, employee profiles, and social network links. |

## Table of contents

- [How it works](#how-it-works)
- [Oceanio Search API](#oceanio-search-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Practical use cases](#practical-use-cases)
- [Why Piloterr?](#why-piloterr)
- [FAQ](#faq)
- [Related scrapers](#related-scrapers)
- [Support](#support)

## How it works

1. **Create a free Piloterr account** and copy your API key from the [dashboard](https://app.piloterr.com).
2. **Send a `GET` (or `POST`) request** to `https://api.piloterr.com/v2/...` with the header `x-api-key: YOUR_API_KEY`.
3. **Receive structured JSON** — Piloterr handles rendering, proxies, retries and parsing.

```bash
export PILOTERR_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

> Every endpoint accepts both `GET` (query string) and `POST` (JSON body with the same fields).

## Oceanio Search API

Search the Ocean.io B2B database by domain to find similar companies, retrieve contact details, employee profiles, and social network links.

`GET | POST https://api.piloterr.com/v2/oceanio/search` · **1 credit per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | Domain name or keyword to search for similar companies in the Ocean.io B2B database. |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/oceanio/search",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "google.com",
    },
    timeout=60,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type OceanioSearch = {
  total?: number;
  people?: {
    "google.com"?: {
      photo?: string;
      last_name?: string;
      first_name?: string;
    }[];
    "yandex.com"?: {
      photo?: string;
      last_name?: string;
      first_name?: string;
    }[];
    "marcombo.com"?: {
      photo?: string;
      last_name?: string;
      first_name?: string;
    }[];
    "wordcruncher.com"?: {
      photo?: string;
      last_name?: string;
      first_name?: string;
    };
  };
  results?: {
    url?: string;
    logo?: string;
    name?: string;
    score?: number;
    domain?: string;
    phones?: {
      number?: string;
      country?: string;
      primary?: boolean;
    }[];
    countries?: string[];
    company_size?: string;
    people_count?: number;
    website_status?: number;
    social_networks?: {
      url?: string;
      platform?: string;
    }[];
  }[];
  companies?: {
    url?: string;
    logo?: string;
    name?: string;
    domain?: string;
    emails?: string[];
    phones?: {
      number?: string;
      country?: string;
    }[];
    countries?: string[];
    company_size?: string;
    people_count?: number;
    social_networks?: {
      url?: string;
      platform?: string;
    }[];
  }[];
};

const params = new URLSearchParams({
  "query": "google.com",
});

const response = await fetch(`https://api.piloterr.com/v2/oceanio/search?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as OceanioSearch;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/oceanio/search
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "google.com"}
```
</details>

### Output example

Example response from the API reference, abridged — real values depend on the page you scrape.

```json
{
  "total": 1,
  "people": {
    "google.com": [
      {
        "photo": "https://media-exp1.licdn.com/dms/image/C4D03AQE1A-2kuJR5ZA/profile-displayphoto-shrink_800_800/0/1580256970663?e=2147483647&v=beta&t=-oVy…",
        "last_name": "example",
        "first_name": "example"
      },
      {
        "photo": "https://media-exp1.licdn.com/dms/image/C4D03AQE29O-Tbfkb_A/profile-displayphoto-shrink_200_200/0/1519574142787?e=1661385600&v=beta&t=9Y2_…",
        "last_name": "example",
        "first_name": "example"
      }
    ],
    "yandex.com": [
      {
        "photo": "https://media-exp1.licdn.com/dms/image/C4D03AQGH7itIEWYS-w/profile-displayphoto-shrink_200_200/0/1607512053171?e=1648684800&v=beta&t=ye8K…",
        "last_name": "example",
        "first_name": "example"
      },
      {
        "photo": "https://media-exp1.licdn.com/dms/image/C4D03AQHkYhsoMlKqEQ/profile-displayphoto-shrink_200_200/0/1607423522134?e=1654732800&v=beta&t=adcI…",
        "last_name": "example",
        "first_name": "example"
      }
    ],
    "marcombo.com": [
      {
        "photo": "https://media.licdn.com/dms/image/v2/C4E03AQFzXVASaHow2g/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/162435…",
        "last_name": "example",
        "first_name": "example"
      },
      {
        "photo": "https://media.licdn.com/dms/image/v2/C4E03AQGdnGevR24XVw/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/154825…",
        "last_name": "example",
        "first_name": "example"
      }
    ],
    "wordcruncher.com": {
      "photo": "https://media.licdn.com/dms/image/v2/D5603AQF5grN6qUa68Q/profile-displayphoto-shrink_200_200/B56ZewOYgIHQAY-/0/1751008250509?e=1770249600…",
      "last_name": "example",
      "first_name": "example"
    }
  },
  "results": [
    {
      "url": "https://yandex.com/",
      "logo": "https://cdn.ocean.io/logos/yandex.com/06e6d49be593e44ad146aca4fd704e7b95827e0c.png",
      "name": "Yandex",
      "score": 1,
      "domain": "yandex.com",
      "phones": [
        {},
        {}
      ],
      "countries": [
        "br",
        "by"
      ],
      "company_size": "I",
      "people_count": 16417,
      "website_status": 3,
      "social_networks": [
        {},
        {}
      ]
    },
    {
      "url": "https://wordcruncher.com/",
      "logo": "https://cdn.ocean.io/logos/wordcruncher.com/8255cc5617d89709428e9d5e932be29d0bf5d0ad.png",
      "name": "WordCruncher",
      "score": 0.6465531587600708,
      "domain": "wordcruncher.com",
      "countries": [
        "us"
      ],
      "company_size": "11-50",
      "people_count": 2,
      "website_status": 1,
      "social_networks": [
        {},
        {}
      ]
    }
  ],
  "companies": [
    {
      "url": "https://www.google.com/",
      "logo": "https://cdn.ocean.io/logos/google.com/695712165c77cdf4b1c56c68bbf5cb6951e03d6c.png",
      "name": "Google",
      "domain": "google.com",
      "emails": [
        "account-withdrawal@google.com"
      ],
      "phones": [
        {},
        {}
      ],
      "countries": [
        "ar",
        "au"
      ],
      "company_size": "I",
      "people_count": 350846,
      "social_networks": [
        {},
        {}
      ]
    }
  ]
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `total` | integer |  |
| `people` | object |  |
| `people.google.com[]` | object[] |  |
| `people.yandex.com[]` | object[] |  |
| `people.marcombo.com[]` | object[] |  |
| `people.wordcruncher.com` | object |  |
| `results[]` | object[] |  |
| `results[].url` | string |  |
| `results[].logo` | string |  |
| `results[].name` | string |  |
| `results[].score` | integer |  |
| `results[].domain` | string |  |
| `results[].phones[]` | object[] |  |
| `results[].countries` | string[] |  |
| `results[].company_size` | string |  |
| `results[].people_count` | integer |  |
| `results[].website_status` | integer |  |
| `results[].social_networks[]` | object[] |  |
| `companies[]` | object[] |  |
| `companies[].url` | string |  |
| `companies[].logo` | string |  |
| `companies[].name` | string |  |
| `companies[].domain` | string |  |
| `companies[].emails` | string[] |  |
| `companies[].phones[]` | object[] |  |

## Code examples in other languages

Ready-to-run examples live in the [`examples/`](examples) folder. Each one reads your key from the `PILOTERR_API_KEY` environment variable.

| Language | Oceanio Search |
|---|---|
| cURL (Bash) | [`search`](examples/curl/search.sh) |
| PHP | [`search`](examples/php/search.php) |
| C# | [`search`](examples/csharp/Search.cs) |
| Go | [`search`](examples/go/search.go) |
| Java | [`search`](examples/java/SearchExample.java) |
| Ruby | [`search`](examples/ruby/search.rb) |
| Node.js | [`search`](examples/nodejs/search.mjs) |

## Practical use cases

- **Lead generation** — Build target account lists from public company data.
- **CRM enrichment** — Keep firmographics, websites and descriptions up to date.
- **Market mapping** — Map competitors and segments across countries and industries.
- **Investment research** — Screen companies, funding and signals for deal flow.
- **Job market analytics** — Track hiring, roles and salaries where available.

## Why Piloterr?

- **No infrastructure** — no proxies, headless browsers or CAPTCHA solving to run yourself.
- **Structured JSON** — stable, documented fields instead of brittle HTML selectors.
- **Pay per request** — transparent credit cost per endpoint, failed requests are retried for you.
- **One API key, hundreds of sources** — Ocean.io plus many other e-commerce, search and company data endpoints in the [Piloterr library](https://www.piloterr.com/library).
- **Any language** — plain HTTPS + JSON, with examples for Python, TypeScript, cURL, PHP, C#, Go, Java, Ruby and Node.js.

## FAQ

### Is it legal to scrape Ocean.io?

Collecting publicly available data is generally allowed in many jurisdictions, but rules depend on your country, the data you collect and how you use it. Avoid personal data unless you have a lawful basis, respect the website's terms where they apply, and get legal advice for your specific use case. This is not legal advice.

### Do I need proxies or a headless browser?

No. Piloterr handles rendering, proxy rotation and retries on its side. You only send an HTTPS request with your `x-api-key` header and receive JSON.

### How much does a request cost?

Credits per call: `/v2/oceanio/search` **1**. See the [Piloterr website](https://www.piloterr.com) for plans.

### What data does the Ocean.io API return?

Each endpoint returns structured JSON: **Oceanio Search** — `total`, `people`, `people.google.com[]`, `people.yandex.com[]`, `people.marcombo.com[]`, `people.wordcruncher.com`.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Related scrapers

- [Company Database Scraper API](https://github.com/piloterr/company-data-api)
- [Crunchbase Scraper API](https://github.com/piloterr/crunchbase-scraper)
- [Europages Scraper API](https://github.com/piloterr/europages-scraper)
- [Fiverr Scraper API](https://github.com/piloterr/fiverr-scraper)
- [G2 Scraper API](https://github.com/piloterr/g2-scraper)
- [github-scraper](https://github.com/piloterr/github-scraper)
- [All Piloterr scrapers on GitHub](https://github.com/piloterr)

## Support

- 💬 Join the [Piloterr Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Browse the [API reference (OpenAPI)](https://app.piloterr.com/openapi) and the [Piloterr library](https://www.piloterr.com/library).
- 🔑 [Get your API key](https://app.piloterr.com).

---

<p align="center">
  <a href="https://www.piloterr.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="Piloterr" height="32">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.piloterr.com">Piloterr</a> — web scraping APIs for e-commerce, search, real estate and more, one API key.</sub>
</p>

<sub>Ocean.io is a trademark of its respective owner. This repository is not affiliated with or endorsed by Ocean.io. Examples are released under the MIT license.</sub>
