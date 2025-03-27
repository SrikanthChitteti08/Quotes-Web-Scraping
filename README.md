# Quotes Web Scraping

This project involves web scraping quotes from [Quotes to Scrape](https://quotes.toscrape.com/) using Python's BeautifulSoup and Requests libraries. The scraped data is then structured into a Pandas DataFrame and saved for further analysis.

## Project Overview
- **Scrape quotes from the first page**
- **Extract details like quote text, author, and tags**
- **Loop through all pages to gather complete data**
- **Store the data in a structured format using Pandas**
- **Save the dataset for further analysis**

## Technologies Used
- **Python**
- **BeautifulSoup** (for web scraping)
- **Requests** (to fetch webpage content)
- **Pandas** (for data handling and storage)
- **TQDM** (for progress tracking)

## Installation
Ensure you have Python installed and then install the required libraries:

```sh
pip install pandas requests beautifulsoup4 tqdm
```

## Usage
Run the Python script or Jupyter Notebook to scrape the quotes and store them in a structured format.

Example snippet:
```python
import pandas as pd
import requests
from bs4 import BeautifulSoup
from tqdm import tqdm

res = requests.get('https://quotes.toscrape.com/')
soup = BeautifulSoup(res.text, 'html.parser')
print(soup.find('span', class_ = 'text').text[1:-1])
```

## Output
The scraped data is stored in a Pandas DataFrame and can be saved as a CSV file for further analysis.

## Conclusion
This project demonstrates the power of web scraping using Python. By leveraging BeautifulSoup and Requests, we efficiently extract structured data from a website. The collected quotes can be further analyzed for sentiment analysis, keyword extraction, or other NLP tasks. This project serves as a foundation for more advanced web scraping applications.
