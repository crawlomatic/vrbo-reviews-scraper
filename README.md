# Vrbo Reviews Scraper & API | Vacation Rental Feedback & Ratings

[![Apify Store](https://img.shields.io/badge/Apify%20Store-View%20Actor-brightgreen?logo=apify)](https://apify.com/misterkhan/vrbo-reviews-scraper)
[![GitHub stars](https://img.shields.io/github/stars/crawlomatic/vrbo-reviews-scraper?style=social)](https://github.com/crawlomatic/vrbo-reviews-scraper)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Python SDK](https://img.shields.io/badge/SDK-Python-3776AB?logo=python&logoColor=white)](https://github.com/apify/apify-client-python)
[![Node.js SDK](https://img.shields.io/badge/SDK-Node.js-339933?logo=node.js&logoColor=white)](https://github.com/apify/apify-client-js)

> Scrape Vrbo property reviews, traveler feedback, star ratings, and host communication scores without getting blocked.

---

## ⚡ Quick Start

You can run this scraper directly via the **[Apify Store Web Console](https://apify.com/misterkhan/vrbo-reviews-scraper)** with zero setup, or integrate it into your Python / Node.js backend using the code below.

### 🐍 Python Quickstart

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

# Initialize the ApifyClient with your API token
# Get your token from https://console.apify.com/account/integrations
client = ApifyClient("YOUR_APIFY_TOKEN")

# Configure input parameters
run_input = {
  "startUrls": [
    {
      "url": "https://www.vrbo.com/1234567"
    }
  ],
  "maxReviews": 50
}

print("🚀 Launching Vrbo Reviews Scraper & API | Vacation Rental Feedback & Ratings on Crawlomatic Engine...")
run = client.actor("misterkhan/vrbo-reviews-scraper").call(run_input=run_input)

# Fetch results from the Actor's default dataset
dataset_items = client.dataset(run["defaultDatasetId"]).list_items().items
print(f"✅ Successfully fetched {len(dataset_items)} records!")

for item in dataset_items[:3]:
    print(item)
```

---

### 🟢 Node.js / JavaScript Quickstart

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

// Initialize the ApifyClient with your API token
const client = new ApifyClient({
    token: 'YOUR_APIFY_TOKEN',
});

// Configure input parameters
const input = {
  "startUrls": [
    {
      "url": "https://www.vrbo.com/1234567"
    }
  ],
  "maxReviews": 50
};

console.log('🚀 Launching Vrbo Reviews Scraper & API | Vacation Rental Feedback & Ratings...');
const run = await client.actor('misterkhan/vrbo-reviews-scraper').call(input);

// Fetch results
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(`✅ Extracted ${items.length} records!`);
console.dir(items.slice(0, 3));
```

---

## What does Vrbo Vacation Rental Reviews Scraper do?

Vrbo Vacation Rental Reviews Scraper is a short-term rental (STR) sentiment and reputation tool that extracts verified guest reviews directly from **Vrbo.com**—capturing numerical star ratings, review titles, full guest commentary, stay dates, traveler group categories, publication timestamps, and host responses.

Whether you manage a vacation rental portfolio across Vrbo and Airbnb, audit guest complaints and seasonal occupancy trends before acquiring a new STR property, or feed guest feedback into AI sentiment models, this scraper delivers clean, structured records in seconds.

> 🛡️ **Zero Proxy Configuration Required:** Anti-blocking and regional routing are **handled automatically out of the box** — just paste your target URLs and click **Start**.

## What data can you extract with Vrbo Vacation Rental Reviews Scraper?

**⭐ Review Rating & Headline** — numeric star `rating` (1.0–5.0), review `title`, and unique review `id` <br>
**💬 Full Guest Commentary** — complete `text` written by the verified vacation rental guest <br>
**🏖️ Property & Listing Provenance** — parsed Vrbo `propertyId` and canonical `propertyUrl` <br>
**👨‍👩‍👧‍👦 Guest & Stay Context** — `reviewerName`, `travelerType` (e.g., Family with young children, Couple, Group of friends), `stayDate`, and `publishedAt` date <br>
**📣 Host / Property Manager Reply** — official `hostResponse` posted by the vacation rental owner or management company, plus `scrapedAt` UTC timestamp <br>

## Why scrape vacation rental reviews from Vrbo?

**💪 Centralize multi-channel STR reputation management** — monitor guest sentiment across your Vrbo listings alongside Airbnb and Booking.com in one unified spreadsheet or BI dashboard <br>
**🕵️ Perform STR acquisition and co-hosting due diligence** — inspect historical review volume, seasonality (`stayDate`), and recurring maintenance complaints before purchasing or onboarding a vacation home <br>
**✨ Identify high-value guest segments** — analyze `travelerType` distributions to see whether families, couples, or large groups drive the highest 5-star reviews in your market <br>
**👍 Zero proxy or account setup** — built-in anti-blocking and proxy rotation work automatically out of the box <br>
**📩 Automate low-rating alerts** — connect recurring runs to Slack, Make, Zapier, or n8n so your property management team can respond to negative reviews immediately <br>

## How do I use Vrbo Vacation Rental Reviews Scraper?

Vrbo Vacation Rental Reviews Scraper is built for fast, zero-configuration operation in Apify Console:

1. Click **Try for free** on the Actor page to open Apify Console.
2. Paste one or more Vrbo property listing URLs into **Vrbo Property URLs** (`startUrls`, for example `https://www.vrbo.com/3757251`).
3. Set **Max Reviews per Property** (`maxReviews`) to choose how many guest reviews to collect.
4. Click **Start** to launch the extraction run.
5. Download your vacation rental review dataset from the **Dataset** tab in Excel, CSV, JSON, or HTML table format.

## Input

Vrbo Vacation Rental Reviews Scraper accepts a simple 2-parameter JSON configuration. Click on the [Input tab](https://apify.com/misterkhan/vrbo-reviews-scraper/input-schema) for the interactive form.

```json
{
  "startUrls": [
    {
      "url": "https://www.vrbo.com/3757251"
    }
  ],
  "maxReviews": 50
}
```

**🏠 `url`** — target Vrbo vacation rental listing URL. Optional when `startUrls` is provided <br>
**🏖️ `startUrls`** — array of Vrbo vacation rental listing URLs (e.g., `https://www.vrbo.com/3757251`) <br>
**🔢 `maxReviews`** — maximum number of guest reviews to extract (default: 50, minimum 1; Free plan runs collect up to 40 reviews per run, while paid Apify plans support unlimited review extraction) <br>

## Output sample

Results are streamed in real time to your default Apify Dataset. Each record represents a verified Vrbo guest review with rating, commentary, stay context, and host reply:

```json
[
  {
    "id": "vrbo_rev_991827",
    "propertyId": "3757251",
    "propertyUrl": "https://www.vrbo.com/3757251",
    "rating": 5.0,
    "title": "Perfect beachfront getaway for our family!",
    "text": "The home was spotless, right on the sand, and the kitchen had everything we needed.",
    "reviewerName": "Michael T.",
    "travelerType": "Family with young children",
    "stayDate": "September 2026",
    "publishedAt": "2026-09-28",
    "hostResponse": "Thank you for staying with us, Michael! We would love to host your family again.",
    "scrapedAt": "2026-10-15T12:00:00Z"
  }
]
```

## How much does it cost to scrape Vrbo reviews?

Vrbo Vacation Rental Reviews Scraper uses **Pay-Per-Event (PPE)** pricing (apify-default-dataset-item) with a `$0.00` startup fee—you only pay for verified guest reviews delivered to your dataset:

**🆓 Free plan** — `$0.005` per review ($5.00 / 1,000 reviews, up to 40 reviews/run) <br>
**🥉 Starter (Bronze) plan** — `$0.0011` per review ($1.10 / 1,000 reviews) <br>
**🥈 Scale (Silver) plan** — `$0.0008` per review ($0.80 / 1,000 reviews) <br>
**🥇 Business+ (Gold) plan** — `$0.0005` per review ($0.50 / 1,000 reviews) <br>

With the monthly free credit on the Apify Free plan, you can extract **up to 1,000 Vrbo guest reviews per month for free**.

> 💡 **Predictable, All-Inclusive Pay-Per-Event Pricing:** There is a **`$0.00` run start fee** and **no separate proxy configuration required**. You only pay the flat per-result rate above for data successfully delivered to your dataset — works out of the box on both **Free** and **Paid** Apify plans.

## How many results can you scrape with Vrbo Vacation Rental Reviews Scraper?

Vrbo Vacation Rental Reviews Scraper can extract **all public guest reviews for any Vrbo property** on paid Apify plans (up to 40 reviews per run on the Free plan). Keep these tips in mind when planning your runs:

- **Direct Vrbo listing URLs (vrbo.com/{propertyId})** — supply specific property listing URLs in `startUrls` to extract their complete guest review history.
- **Rating-only submissions** — if a guest leaves a star rating on Vrbo without writing a body comment, `text` will return an empty string while preserving `rating`, `reviewerName`, `stayDate`, and `publishedAt`.
- **Multi-property STR portfolios** — pass dozens of Vrbo property URLs in `startUrls` to audit your entire vacation rental portfolio or local market comp set in one run.

## Want to scrape Airbnb, Booking.com, Zillow, or ForSaleByOwner?

Combine VRBO Reviews Scraper with our published short-term rental, hospitality, and US real estate Actors:

🏡 **[Airbnb Reviews Scraper](https://apify.com/misterkhan/airbnb-reviews-scraper)** — extract verified Airbnb guest reviews, star ratings, translated review text, and host replies (From $0.50 / 1K) <br>
🏨 **[Booking.com Reviews Scraper](https://apify.com/misterkhan/booking-reviews-scraper)** — scrape hotel guest reviews, separated positive/negative comments, stay dates, and room types (From $0.50 / 1K) <br>
🏡 **[Zillow Search Scraper](https://apify.com/misterkhan/zillow-scraper)** — extract US homes for sale, rentals, sold prices, Zestimates, beds/baths, and coordinates (From $0.90 / 1K) <br>
🇺🇸 **[ForSaleByOwner.com US FSBO Scraper](https://apify.com/misterkhan/forsalebyowner-us-scraper)** — scrape direct commission-free US homeowner property listings and seller details (From $0.75 / 1K) <br>
## Integrations and Vrbo Vacation Rental Reviews Scraper

Vrbo Vacation Rental Reviews Scraper connects directly with your property management spreadsheets, BI tools, and automation workflows through [Apify integrations](https://apify.com/integrations):

- **No-Code Automation** — trigger instant Slack/email alerts on low-star reviews or draft AI host responses via Make, Zapier, or n8n.
- **Spreadsheets & Warehouses** — sync guest reviews straight into Google Sheets, Airtable, BigQuery, Snowflake, or PostgreSQL.
- **Webhooks** — send automated HTTP webhook payloads to your STR dashboard whenever a run finishes.

## Using Vrbo Vacation Rental Reviews Scraper with the Apify API

You can launch review runs and fetch dataset items programmatically using the official `apify-client` libraries for **Node.js** and **Python**, or connect this Actor to AI hospitality agents via the **Apify MCP Server** (`https://mcp.apify.com`).

Check the [API tab](https://apify.com/misterkhan/vrbo-reviews-scraper/api) for ready-to-copy Node.js, Python, and cURL code snippets.

## Frequently asked questions about Vrbo Vacation Rental Reviews Scraper

**🏖️ Can I pass multiple Vrbo property URLs in a single run? <br>**
Yes. Add as many Vrbo property URLs as you need to `startUrls` and the scraper will extract guest reviews across every listing in your batch.

**📣 Does the scraper include host and property manager replies? <br>**
Yes. Whenever a host or property manager replies to a guest review on Vrbo, the full response is captured in the `hostResponse` field.

**🛡️ Do I need to configure proxies or a Vrbo account? <br>**
**No — everything works out of the box with zero setup.** Regional routing, session management, and anti-blocking are handled automatically so you do not need to configure custom proxy settings.

## Is it legal to scrape public guest reviews from Vrbo?

Our scrapers are ethical and only extract publicly available guest ratings, review comments, and host responses displayed on public Vrbo property pages. They do not access private reservation details or personal account data. For more details on the legality of web scraping, read Apify's guide on [is web scraping legal](https://blog.apify.com/is-web-scraping-legal/).

## Your feedback

We keep this Actor under active maintenance. If a run finishes successfully but returns fewer results than you expected, hangs, or errors — please **open an Issue before posting a public review** so we can diagnose and fix it for you.

**🛠️ How to report** — Use the Actor’s [Issues tab](https://apify.com/misterkhan/vrbo-reviews-scraper/issues/open) in Apify Console. Include the run ID, your input JSON, and what you expected vs. what you got. <br>
**⏱️ Response time** — We aim to reply within 24 hours on business days. <br>
**⭐ Reviews** — Happy with the results? A short positive review helps other users find a reliable scraper. Ran into a problem? Open an Issue first — we’ll work with you to resolve it before you leave a rating. <br>


---

## 🛡️ Architecture & Engine Reliability

This scraper runs on the **[Crawlomatic Engine](https://crawlomatic.com)**:
- **Zero Proxy Configuration:** Intelligent residential and datacenter proxy rotation with automated regional ccTLD binding.
- **WAF Bypass Engine:** Autonomous challenge solving for Cloudflare Turnstile, DataDome, PerimeterX, Kasada, and Akamai.
- **Pay-Per-Event (PPE) Pricing:** Transparent pay-as-you-go pricing with \$0 starting fee.

## 📄 License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Developed & Maintained by **[Crawlomatic](https://crawlomatic.com)**.
