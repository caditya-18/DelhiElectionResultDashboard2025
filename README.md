# Delhi Election 2025 - Data Scraping & Processing

## Overview
This repository contains Python scripts to scrape and process election-related data for the **Delhi Election 2025**. The scripts leverage **Selenium** for web scraping and **pdfplumber** for extracting tabular data from election-related PDF files. The extracted data is stored in CSV files for further analysis.

## Features
- **Web Scraping with Selenium**: Extracts constituency-wise election results from the **Election Commission of India (ECI)** website.
- **PDF Data Extraction**: Extracts parliamentary constituency-wise elector data from PDF reports.
- **Data Processing**: Cleans and structures data for easy analysis.
- **CSV Export**: Saves extracted data in CSV format.

---

## Project Structure
```
DelhiElection2025/
│-- election_scraper.py    # Web Scraping Script
│-- pdf_data_extractor.py  # PDF Data Extraction Script
│-- delhi_election_results.csv  # Scraped Election Results
│-- PC_wise_Electors.csv  # Extracted PDF Data
│-- README.md  # Project Documentation
```

---

## Requirements
Ensure you have the following dependencies installed:
```sh
pip install selenium pandas pdfplumber
```

Also, **download and set up** ChromeDriver to run Selenium.

---

## Scripts & Functionalities
### **1. Election Results Scraper** (`election_scraper.py`)
This script scrapes constituency-wise election results from the **ECI results website**.

#### **How it Works:**
1. Iterates through **70 constituencies**.
2. Extracts tabular data (Candidate Name, Party, Votes, etc.).
3. Saves data in a **CSV file** (`delhi_election_results.csv`).

#### **Key Code Snippets:**
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
import pandas as pd
import time

# Setup WebDriver
driver = webdriver.Chrome()

# Loop through constituencies
for num in range(1, 71):
    url = f"https://results.eci.gov.in/ResultAcGenFeb2025/ConstituencywiseU05{num}.htm"
    driver.get(url)
    time.sleep(3)
```

#### **Output Format:**
| Constituency No | S.N. | Candidate | Party | EVM Votes | Postal Votes | Total Votes |
|----------------|------|-----------|-------|-----------|--------------|-------------|
| 1             | 1    | Candidate A | Party X | 20000 | 500 | 20500 |
| 1             | 2    | Candidate B | Party Y | 18000 | 600 | 18600 |

---

### **2. PDF Data Extraction** (`pdf_data_extractor.py`)
This script extracts data from a **PDF file** containing parliamentary constituency-wise elector data.

#### **How it Works:**
1. Opens the PDF using **pdfplumber**.
2. Extracts table rows while **handling missing values**.
3. Saves the structured data in a **CSV file** (`PC_wise_Electors.csv`).

#### **Key Code Snippets:**
```python
import pdfplumber
import pandas as pd

pdf_path = "D:/DelhiElection2025/PC_wise_Electors_With_AC.pdf"
data = []

with pdfplumber.open(pdf_path) as pdf:
    for page in pdf.pages:
        table = page.extract_table()
        if table:
            for row in table:
                if row[0] == "PC No.":
                    continue
                data.append(row[:8])
```

#### **Output Format:**
| PC No | PC Name  | AC No | AC Name   | Male  | Female | Third Gender | Total   |
|-------|---------|-------|----------|-------|--------|--------------|---------|
| 1     | Delhi   | 10    | XYZ Nagar | 120000 | 110000 | 500          | 230500 |

---

## How to Run the Scripts

### **1. Run the Election Results Scraper**
```sh
python election_scraper.py
```
- This will generate `delhi_election_results.csv` with the scraped election data.

### **2. Run the PDF Data Extractor**
```sh
python pdf_data_extractor.py
```
- This will generate `PC_wise_Electors.csv` containing elector details.

---

## Future Enhancements
✔ Automate data updates at regular intervals.  
✔ Improve error handling & logging.  
✔ Integrate with visualization tools like **Matplotlib/Power BI**.  
✔ Store data in a **SQL database** for better querying.  

---

## Contribution
- Feel free to fork the repo and submit **pull requests**.
- Report any **issues or improvements** under the Issues section.

---

## License
This project is **open-source** under the MIT License.

---

### **Contact**
For queries, reach out via [GitHub Issues](https://github.com/your-repo/issues).

---

### 🚀 Keep Exploring & Happy Coding! 🚀

