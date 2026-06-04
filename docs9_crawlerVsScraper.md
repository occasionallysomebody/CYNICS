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
>Are we trying to build a dashboard or research ways to improve crawlers?
- some other tools I found
- [scrapling](https://scrapling.readthedocs.io/en/latest/index.html#star-history): self healing web scraping framework (traditionally, one misplaced class/div can break your pipelin, scrapling fixes this)
- exa: apis for ai agents

Firecrawl: The Web Data Engine

Firecrawl specializes in converting websites into clean, large language model-ready data (like Markdown or JSON). [[1](https://www.firecrawl.dev/blog/choosing-web-scraping-tools), [2](https://www.youtube.com/watch?v=2s2aR4rOQ8Y)]

- **What it does:** Crawls entire websites, handles dynamic JavaScript (SPA/React sites), takes screenshots, and performs multi-engine searches. [[1](https://www.youtube.com/watch?v=wAoJdpM_eTM), [2](https://www.youtube.com/watch?v=2s2aR4rOQ8Y)]
- **Why it's unique:** Instead of using brittle CSS selectors or XPaths, you can use natural language prompts to extract specific structured data from complex pages. [[1](https://www.firecrawl.dev/blog/fine-tuning-deepseek)]
- **Integration:** It seamlessly drops into RAG pipelines and AI agent workflows. [[1](https://www.youtube.com/watch?v=2s2aR4rOQ8Y), [2](https://www.firecrawl.dev/blog/choosing-web-scraping-tools)]
- **Pricing:** Usage is based on page credits, and it features an open-source version for self-hosting. [[1](https://www.firecrawl.dev/alternatives/firecrawl-vs-apify), [2](https://www.firecrawl.dev/glossary/web-scraping-apis/what-is-open-source-web-scraping)]

DeepSeek: The Intelligence Layer

DeepSeek is a family of state-of-the-art LLMs (like the reasoning-focused DeepSeek R1 and V3) known for highly capable, low-cost APIs. [[1](https://www.revechat.com/blog/deepseek-vs-qwen/), [2](https://www.inferless.com/learn/the-ultimate-guide-to-deepseek-models), [3](https://medium.com/@amirabdallahpfe/lets-build-a-deepsearch-agent-using-agno-firecrawl-nebuis-ai-deepseek-v3-and-streamlit-20cf5231f511), [4](https://www.youtube.com/watch?v=WkLdLJJzV1k), [5](https://www.cbinsights.com/company/deepseek/alternatives-competitors)]

- **What it does:** Understands context, reasons through complex queries, and generates human-like text or code.
- **Why it's unique:** DeepSeek provides top-tier reasoning and model performance at a fraction of the cost of legacy models (like GPT-4o or Claude 3.5).
- **Integration:** Used to process, summarize, and act on raw text inputs

- Exa, firecrawl, deepseek flow

The idea: feed apis to exa, ask for similar 