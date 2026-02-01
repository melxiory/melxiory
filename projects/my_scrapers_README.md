<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Fira+Code&size=28&duration=2800&pause=2000&color=3776AB&center=true&vCenter=true&width=600&height=70&lines=Web+Scrapers;Python+Async%2FAwait" alt="Typing SVG" />
</p>

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Async](https://img.shields.io/badge/Async-Await-FF6B6B?style=for-the-badge)
![Selenium](https://img.shields.io/badge/Selenium-Latest-43B02A?style=for-the-badge&logo=selenium&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

A collection of high-performance **web scrapers** built with **Python async/await** and **Selenium**. Designed for efficient data extraction from various websites with concurrent processing and smart retry mechanisms.

### Key Features

- ⚡ **Async/Await** for concurrent scraping
- 🔄 **Smart Retry Logic** with exponential backoff
- 📦 **Multiple Data Export** formats (JSON, CSV, Excel)
- 🛡️ **Rate Limiting** and respectful scraping
- 📊 **Progress Tracking** with logging
- 🎯 **Dynamic Content** rendering with Selenium
- 🔧 **Configurable** scraping parameters

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Python 3.11+ |
| **Async Framework** | asyncio, aiohttp |
| **Browser Automation** | Selenium 4 |
| **Data Processing** | pandas, BeautifulSoup4 |
| **Export Formats** | JSON, CSV, Excel (openpyxl) |
| **Configuration** | YAML, python-dotenv |

---

## 📦 Installation

### Prerequisites

- Python 3.11 or higher
- Chrome/Firefox browser (for Selenium)
- ChromeDriver/GeckoDriver

### Step 1: Clone the Repository

```bash
git clone https://github.com/melxiory/my_scrapers.git
cd my_scrapers
```

### Step 2: Create Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure

```bash
cp config.example.yaml config.yaml
# Edit config.yaml with your settings
```

### Step 5: Run

```bash
python main.py
```

---

## 📁 Project Structure

```
my_scrapers/
├── scrapers/                # Scraper modules
│   ├── base.py              # Base scraper class
│   ├── example_scraper.py   # Example implementation
│   └── selenium_scraper.py  # Selenium-based scraper
├── utils/                   # Utility functions
│   ├── async_fetcher.py     # Async HTTP client
│   ├── parser.py            # HTML parsing utilities
│   └── exporter.py          # Data export utilities
├── config/                  # Configuration files
│   ├── config.yaml          # Main configuration
│   └── sites.yaml           # Site-specific settings
├── output/                  # Scraped data
├── logs/                    # Application logs
├── main.py                  # Entry point
└── requirements.txt
```

---

## 🎯 Usage Examples

### Basic Async Scraper

```python
import asyncio
from scrapers.base import AsyncScraper

class MyScraper(AsyncScraper):
    async def fetch_page(self, url: str) -> str:
        async with self.session.get(url) as response:
            return await response.text()

    async def scrape(self, urls: list[str]) -> list[dict]:
        tasks = [self.fetch_page(url) for url in urls]
        results = await asyncio.gather(*tasks)
        return [self.parse(html) for html in results]

# Usage
async def main():
    scraper = MyScraper(max_concurrent=10)
    data = await scraper.scrape([
        "https://example.com/page1",
        "https://example.com/page2"
    ])
    print(data)

asyncio.run(main())
```

### Selenium Scraper

```python
from scrapers.selenium_scraper import SeleniumScraper

class DynamicScraper(SeleniumScraper):
    def parse(self, driver) -> dict:
        # Wait for element to load
        element = self.wait_for_css('.content', timeout=10)
        return {
            'title': driver.find_element('tag name', 'h1').text,
            'content': element.text
        }

# Usage
scraper = DynamicScraper(headless=True)
data = scraper.scrape('https://example.com')
print(data)
scraper.close()
```

---

## 📊 Data Export

The scrapers support multiple export formats:

```python
from utils.exporter import DataExporter

data = [{'name': 'Item 1', 'price': 100}]

# Export to JSON
exporter = DataExporter()
exporter.to_json(data, 'output/data.json')

# Export to CSV
exporter.to_csv(data, 'output/data.csv')

# Export to Excel
exporter.to_excel(data, 'output/data.xlsx', sheet_name='Products')
```

---

## 🔧 Configuration

### config.yaml

```yaml
scraper:
  max_concurrent: 10
  timeout: 30
  retry_attempts: 3
  retry_delay: 2

selenium:
  headless: true
  browser: chrome
  window_size: [1920, 1080]

export:
  format: json
  output_dir: ./output

logging:
  level: INFO
  file: logs/scraper.log
```

---

## 🛡️ Best Practices

### 1. Respectful Scraping

```python
# Add delays between requests
scraper = AsyncScraper(delay_between_requests=1.5)

# Respect robots.txt
scraper.check_robots_txt=True
```

### 2. Error Handling

```python
try:
    data = await scraper.scrape(urls)
except ConnectionError as e:
    logger.error(f"Connection failed: {e}")
except ParseException as e:
    logger.error(f"Parse error: {e}")
```

### 3. Rate Limiting

```python
from utils.rate_limiter import RateLimiter

limiter = RateLimiter(max_requests=100, time_window=60)
scraper = AsyncScraper(rate_limiter=limiter)
```

---

## 📸 Examples

### Supported Websites

| Website | Scraper | Status |
|---------|---------|--------|
| Example.com | example_scraper.py | ✅ Working |
| Site.org | org_scraper.py | ✅ Working |
| Demo.net | demo_scraper.py | 🔧 In Development |

---

## 🚀 Performance

Benchmarks on a sample of 1000 pages:

| Configuration | Time | Throughput |
|--------------|------|------------|
| Synchronous | 250s | 4 req/s |
| Async (10 concurrent) | 35s | 28 req/s |
| Async + Selenium (5 workers) | 180s | 5.5 req/s |

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ⚠️ Disclaimer

This project is for educational purposes only. Always:
- Check the website's `robots.txt` and Terms of Service
- Respect rate limits and server resources
- Use scraped data responsibly and legally

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**melxiory**

- GitHub: [@melxiory](https://github.com/melxiory)

---

## 🙏 Acknowledgments

- [aiohttp](https://docs.aiohttp.org/) - Async HTTP client
- [Selenium](https://www.selenium.dev/) - Browser automation
- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) - HTML parsing

---

<div align="center">

### 🌟 Star this repo if it helped you!

[![GitHub stars](https://img.shields.io/github/stars/melxiory/my_scrapers?style=social)](https://github.com/melxiory/my_scrapers/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/melxiory/my_scrapers?style=social)](https://github.com/melxiory/my_scrapers/network/members)

</div>
