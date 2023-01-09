# Job Listing with GCP

### Introduction

This blog will give you a good insight into the pipeline to fetch jobs around the US or your preferred location, saving them into BigQuery tables, and iterate this process for you every day or at specified intervals.

### Pre-requisites

You should have a GCP account with admin access or a privileged service account to perform tasks. I will be using Python language for it.

### Procedures

This project consists of three `.py` files named as `scraper.py` , `server.py` , `scheduler.py` .

1. codes for `scraper.py`
    

```python
from bs4 import BeautifulSoup
import requests

# Fetch the job listings from the website, you can give any website for job search by keeping scrapping in mind
response = requests.get('https://www.jobboard.com/jobs/data-engineer')
html = response.text

# Parse the HTML to extract the job data using bs4(BeautifulSoup)
soup = BeautifulSoup(html, 'html.parser')
jobs = []
for div in soup.find_all('div', class_='job-listing'):
    title = div.find('h2').text
    company = div.find('h3').text
    location = div.find('span', class_='location').text
    jobs.append({'title': title, 'company': company, 'location': location})

# Send the job data to the server, I used dummy site to show not the original 
requests.post('https://mysite.com/save_jobs', json=jobs)
```

1. codes for `server.py`
    

```python
from google.cloud import bigquery

# function made to save fetched data into table
def save_jobs(request):
    request_json = request.get_json() # Extract the job data from the request
    jobs = request_json['jobs']

    # Create a BigQuery client
    client = bigquery.Client()

    # Create a new dataset
    dataset = bigquery.Dataset(client.dataset('job_data'))
    dataset.location = 'US'
    dataset = client.create_dataset(dataset)

    # Create a new table in the dataset
    table = bigquery.Table(dataset.table('job_listings_jobboard'), schema=[
        bigquery.SchemaField('Title', 'STRING'),
        bigquery.SchemaField('Company', 'STRING'),
        bigquery.SchemaField('Location', 'STRING')
    ])
    table = client.create_table(table)

    # Load the data into the table
    errors = client.insert_rows(table, rows=jobs)
    if errors:
        print(errors)
```

1. codes for `scheduler.py`
    

```python
from google.cloud import scheduler

# setup a Cloud Scheduler client
client = scheduler.Client()

# Create a new job
job = client.create_job(name='fetch_jobs_data_engineer', body={
    'schedule': '* 6 * * *', # change this schedule as per yours
    'time_zone': 'UTC',
    'http_target': {
        'uri': 'https://mysite.com/scraper', # I used dummy site uri
        'http_method': 'POST'
    }
})
```