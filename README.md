# Job Market Analysis Using Python, SQL & Pandas

A data analysis project that collects job-market data from the Adzuna Jobs API, stores the results, and performs analysis using Python/Pandas and SQL.

## Project Overview

This project was created to practice an end-to-end data analysis workflow:

1. Fetch job listings from an API
2. Collect relevant fields from each job posting
3. Store the data in a Pandas DataFrame
4. Export job data for further analysis
5. Perform data cleaning and exploratory analysis
6. Use SQL for querying and analysis
7. Generate insights from job-market data

## Technologies Used

- Python
- Requests
- Pandas
- NumPy
- SQLite
- SQL
- Jupyter Notebook

## Project Files

```text
job-market-analysis/
│
├── job data analyzer using pyhton.ipynb   # Python/API data collection & analysis
├── work using sql.ipynb                   # SQL analysis
├── jobs_data.csv                          # Job listing dataset
├── job_market_analysis.csv                # Analysis/output dataset
├── job_market.db                          # SQLite database
│
├── adzuna_job_scraper.py                  # API extraction script
├── requirements.txt                       # Python dependencies
├── .gitignore                             # Files that should not be uploaded
├── .env.example                           # API credential template
└── README.md                              # Project documentation
```

## API Data Collection

The project uses the Adzuna Jobs API to retrieve job listings.

The API request collects multiple pages of results and extracts:

- Job title
- Company
- Location
- Job category
- Job description

Example workflow:

```python
jobs = []

for page in range(1, 21):
    url = f"https://api.adzuna.com/v1/api/jobs/in/search/{page}"

    response = requests.get(
        url,
        params={
            "app_id": APP_ID,
            "app_key": APP_KEY,
            "results_per_page": 10
        },
        timeout=30
    )

    response.raise_for_status()
    data = response.json()

    for job in data.get("results", []):
        jobs.append({
            "title": job.get("title"),
            "company": job.get("company", {}).get("display_name"),
            "location": job.get("location", {}).get("display_name"),
            "category": job.get("category", {}).get("label"),
            "description": job.get("description")
        })
```

## Important: API Security

**Do not upload your real Adzuna API credentials to GitHub.**

Store them in a local `.env` file or environment variables.

Create a `.env` file locally:

```text
ADZUNA_APP_ID=your_app_id
ADZUNA_APP_KEY=your_app_key
```

The `.env` file is ignored by Git through `.gitignore`.

If an API key has already been exposed publicly, revoke/rotate it from the API provider before pushing the project to GitHub.

## Installation

Clone the repository:

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd job-market-analysis
```

Create a virtual environment:

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Configuration

Create a `.env` file in the project root:

```text
ADZUNA_APP_ID=your_app_id
ADZUNA_APP_KEY=your_app_key
```

Then run:

```bash
python adzuna_job_scraper.py
```

## Analysis

The collected data can be analyzed using:

- Pandas
- SQL
- SQLite
- Excel/CSV
- Jupyter Notebook

Possible analysis questions include:

- Which job titles appear most frequently?
- Which companies have the most listings?
- Which locations have the highest number of jobs?
- Which job categories are most common?
- What skills/keywords occur frequently in job descriptions?
- How can job-market data be filtered and summarized using SQL?

## What I Learned

This project demonstrates practical experience with:

- REST API data extraction
- JSON response handling
- Python requests
- Pandas DataFrames
- Data cleaning
- CSV data handling
- SQLite databases
- SQL queries
- Exploratory data analysis
- Structuring a small data-analysis project

## Disclaimer

The job data is obtained from the Adzuna API and may change over time. The project is intended for learning and data-analysis practice.
