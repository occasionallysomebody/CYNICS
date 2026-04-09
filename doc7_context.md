# Project Overview

Build an ESG-compliant web crawler for competitive environmental monitoring in the oil & gas sector, with a focus on independent verification methods for Azerbaijan's oil and gas operations. The crawler should extract structured data from regulatory documents, environmental monitoring sources, and ESG reporting standards.

## Input Data

You will receive a CSV file with the following structure:

```csv
source_name,url,category,tags,doc_type,update_frequency,priority,notes
```

### Column Definitions:
- **source_name**: Human-readable name of the source
- **url**: Full URL to the document or data source
- **category**: Main category (regulatory, environmental_monitoring, esg_standards, academic_research, etc.)
- **tags**: Comma-separated tags including:
  - `observed_data`: Independent satellite/sensor monitoring data
  - `state_derived_data`: Government or state-provided data
  - `ecology_public_relations`: Environmental/health impact data
  - `regulatory_compliance`: Compliance frameworks and requirements
  - `disclosure_standards`: ESG/sustainability reporting standards
- **doc_type**: File type (PDF, HTML, API, CSV, etc.)
- **update_frequency**: How often the source updates (daily, monthly, annual, static)
- **priority**: Crawl priority (high, medium, low)
- **notes**: Additional context about the source

## Key Source Categories

### 1. Regulatory Bodies & Compliance Documents
- **SEC (Securities and Exchange Commission)**: Climate disclosure rules, oil & gas reporting modernization
- **EPA (Environmental Protection Agency)**: Methane emissions standards, compliance guides, super emitter programs
- **FERC (Federal Energy Regulatory Commission)**: Natural gas project environmental guidelines
- **BLM/BOEM/BSEE**: Federal land and offshore energy management

### 2. ESG & Sustainability Standards
- **GRI (Global Reporting Initiative)**: GRI 11 Oil & Gas Sector, GRI 102 Climate Change, GRI 103 Energy, GRI 101 Biodiversity
- **SASB (Sustainability Accounting Standards Board)**: Oil & Gas Exploration/Production and Services standards
- **ISSB Framework**: Integrated sustainability disclosure

### 3. Independent Environmental Monitoring
- **Satellite Data Sources**: Sentinel-1 SAR imagery for oil spill detection (Copernicus Hub)
- **Transparent World**: Independent Caspian Sea oil monitoring using satellite remote sensing
- **Academic Research**: Peer-reviewed studies on Caspian Sea pollution, biological sampling (sturgeon hydrocarbon analysis)

### 4. Multilateral Organizations & NGOs
- **World Bank**: Economic and environmental assessments of Azerbaijan
- **Global Witness**: Gas flaring pollution and health impact reports
- **Space Research Institute (Russia)**: Satellite-based environmental databases

## Crawler Requirements

### Core Functionality:
1. **CSV Ingestion**: Read and parse the provided CSV file with all source metadata
2. **Multi-Format Support**: Handle PDFs, HTML pages, structured data APIs
3. **Tag-Based Filtering**: Allow filtering sources by tags (e.g., only crawl `observed_data` sources)
4. **Priority-Based Crawling**: Process high-priority sources first
5. **Rate Limiting**: Respect robots.txt and implement polite crawling delays
6. **Error Handling**: Log failed requests, retry with exponential backoff

### Data Extraction:
1. **PDF Processing**: Extract text, tables, and structured data from regulatory PDFs
2. **HTML Scraping**: Parse web pages for specific data fields (emissions data, compliance metrics)
3. **Structured Data**: Extract key metrics aligned with ESG frameworks:
   - GHG emissions (Scope 1, 2, 3)
   - Methane emissions and flaring data
   - Oil spill incidents and volumes
   - Water usage and contamination
   - Biodiversity impact assessments
   - Compliance violations and enforcement actions

### Output Format:
Create structured JSON or CSV outputs with:
- Source metadata (URL, date accessed, source type)
- Extracted data fields
- Data quality indicators (observed vs. state-derived)
- Timestamps and versioning
- Citation information for traceability

## Technical Implementation Guidelines

### Libraries to Use:
- **requests** or **httpx**: HTTP requests
- **beautifulsoup4** or **lxml**: HTML parsing
- **PyPDF2** or **pdfplumber**: PDF text extraction
- **pandas**: Data manipulation and CSV handling
- **selenium** or **playwright** (if needed): JavaScript-heavy sites
- **ratelimit** or **tenacity**: Rate limiting and retries

### Architecture Recommendations:
1. **Modular Design**: Separate modules for CSV parsing, URL fetching, content extraction, and data storage
2. **Configuration**: Load source CSV at runtime, allow command-line filtering by tags/priority
3. **Logging**: Comprehensive logging of crawl progress, errors, and data quality issues
4. **Caching**: Cache downloaded documents to avoid re-downloading
5. **Incremental Updates**: Track last crawl date and only update changed sources

### Special Considerations:

#### For Satellite/Remote Sensing Data:
- Copernicus Hub API may require authentication
- Transparent World data may be available via their Telegram channel or web interface
- Consider spatial and temporal dimensions (lat/lon, date ranges)

#### For Regulatory Documents:
- SEC EDGAR filings follow specific XML/HTML structure
- EPA documents may require navigating nested folder structures
- Extract specific sections (e.g., "Climate-Related Risks", "Emissions Data")

#### For ESG Standards:
- GRI and SASB provide PDF standards documents with specific disclosure requirements
- Map extracted data to standard disclosure frameworks (e.g., GRI 305-1: Direct GHG emissions)

## Data Quality & Bias Considerations

Prioritize sources with these characteristics:
- **Independent Verification**: Satellite imagery, academic peer review, third-party monitoring
- **Methodology Transparency**: Clear documentation of measurement methods
- **Cross-Validation**: Multiple independent sources confirming findings
- **Temporal Consistency**: Regular monitoring over time

Flag potential bias in:
- State-provided data from Azerbaijan government sources
- Industry self-reporting without third-party verification
- Single-source claims without corroboration

## Example Workflow

1. **Load CSV**: Read source list with pandas
2. **Filter by Tags**: Select sources with `observed_data` + `regulatory_compliance` tags
3. **Prioritize**: Sort by priority (high → low)
4. **Crawl**: 
   - For each URL, identify document type
   - Download and cache document
   - Extract relevant data based on source category
5. **Structure Output**: Create standardized data records with metadata
6. **Export**: Save to JSON/CSV with timestamps and source citations
7. **Generate Report**: Summary of data collected, quality flags, and gaps

## Monitoring & Validation

Track these metrics:
- URLs successfully crawled vs. failed
- Data freshness (last update date from source)
- Coverage across source categories
- Conflicts between sources (e.g., different emission values)
- Missing data fields per ESG framework

## Ethical & Legal Compliance

- Respect copyright and terms of service
- Use public/open-access sources or obtain proper permissions
- Implement robots.txt compliance
- Rate limit to avoid overwhelming servers
- Attribute all data to original sources with proper citations

## Expected Deliverables

1. **Web Crawler Script**: Python notebook or script in Google Colab
2. **Structured Data Output**: JSON or CSV with extracted ESG metrics
3. **Data Quality Report**: Summary of sources crawled, data quality indicators, and gaps
4. **Documentation**: Code comments and usage instructions
5. **Visualization (Optional)**: Simple charts showing temporal trends or geographic distribution

## Success Criteria

The crawler should successfully:
- Process all URLs from the CSV input
- Extract structured data aligned with GRI/SASB frameworks
- Distinguish between observed and state-derived data
- Generate timestamped, citable outputs
- Handle errors gracefully and log issues
- Complete a full crawl cycle within reasonable time (< 2 hours for ~50 sources)

## Notes on Azerbaijan Oil & Gas Context

The specific use case focuses on:
- Monitoring Caspian Sea oil pollution (Oil Rocks region, Sangachal terminal)
- Validating government-reported vs. independently observed environmental data
- Tracking compliance with international ESG standards
- Assessing health impacts of gas flaring on nearby populations (880,000+ at risk)
- Comparing Azerbaijan's practices to US regulatory standards (as benchmark)

Key entities to monitor:
- BP Azerbaijan (Sangachal terminal operator)
- SOCAR (State Oil Company of Azerbaijan Republic)
- Azerbaijan Ministry of Ecology and Natural Resources
- Independent validators: Transparent World, Shirshov Institute of Oceanology, academic researchers

---

**IMPORTANT**: You will receive the CSV file as a direct upload. Load it using `pandas.read_csv()` and begin processing immediately. The CSV contains all necessary metadata to configure the crawler dynamically.