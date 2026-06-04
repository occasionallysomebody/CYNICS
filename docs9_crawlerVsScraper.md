- crawler extracts raw unformatted data
- scrapper formats
> From Google: Here is a quick breakdown of how they differ:
> - **Web Crawler (Spider/Bot):** Best for **discovery and navigation**. It systematically browses the web—like Googlebot indexing sites—to map out URLs, follow links, and build an organized directory of content. [[1](https://www.nimbleway.com/blog/web-crawling-vs-web-scraping), [2](https://www.promptcloud.com/blog/complete-guide-to-web-crawling/), [3](https://duplicator.com/web-crawler-comparison/), [4](https://www.ematicsolutions.com/crawling-indexing-search-engine/), [5](https://www.postaffiliatepro.com/faq/why-are-web-crawlers-called-spiders/)]
>   - **Web Scraper:** Best for **data extraction and analytics**. It targets specific websites to pull out raw data (e.g., product prices, user reviews, or financial metrics) and exports it into a structured format like a CSV, JSON, or database for analysis. [[1](https://www.browse.ai/blog/web-scraping-vs-web-crawling-whats-the-difference), [2](https://zenscrape.com/how-can-a-web-scraper-get-information-on-your-competitors/), [3](https://www.promptcloud.com/blog/web-scraper-api-to-automate-data-collection/), [4](https://www.browse.ai/blog/web-scraping-vs-web-crawling-whats-the-difference), [5](https://medium.com/@Excellarate/web-scraping-introduction-applications-and-best-practices-c7e5eb06c07e)]

- **lockfiles** let you update dependency versions without breaking other people's code
- techdebt.md
- implementation_plan.md
- goal.md (CEO.md)
- agent_instructions.md
- pipeline_instructions.md
- python's version of javadocs: sphinx 
---
Try to use free apis and feeds instead of crawling urls:
- **EIA API** — free, has Azerbaijan production data, Caspian region reports
- **World Bank API** — free, country indicators, governance scores
- **SOFAZ (State Oil Fund of Azerbaijan)** — publishes reports, has an RSS feed
- **EITI (Extractive Industries Transparency Initiative)** — structured data on oil revenues
- **UN Comtrade API** — free, trade flow data
- **ReliefWeb API** — free, humanitarian/risk reports by country
- **GDELT Project** — free, massive event database pulling from news globally, has an Azerbaijan filter
- **Google News RSS** — `rss.app` or direct Google News URL filtered to "Azerbaijan energy" gives you structured headlines for free

- structured information reduces parsing

Potential research areas:
#### What crawler research actually involves

There are a few distinct problems your group might care about:

**Discovery** — how do you find relevant pages you didn't know existed? Link following, sitemap parsing, search API seeding, feed monitoring. This is where interesting research lives around relevance scoring and frontier prioritization.

**Extraction quality** — Trafilatura is already best-in-class for boilerplate removal. The research frontier here is more about structured extraction from messy real-world HTML, tables, PDFs.

**Autonomous judgment** — deciding _what's worth crawling_ is an open problem. Using an LLM to score relevance before fetching, or to generate new seed queries, is genuinely novel and not a solved problem.

**Scale and politeness** — less interesting research, more engineering. Unless your group specifically studies crawl ethics or web infrastructure.

Research is different from building an enterprise grade product
- some other tools I found
- scrapling: self healing web scraping framework (traditionally, one misplaced class/div can break your pipelin,)