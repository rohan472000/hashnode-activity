# Covid cases fetching with GCP

### Introduction

This blog is all about a pipeline that fetches daily covid data as it is orchestrated by apache-airflow and saves the data into the BigQuery table.

### Pre-requisites

You should have a GCP account with admin or privileged access, and apache-airflow installed or you can use cloud composers also(GCP).

### Procedures

This project consists of two files named as `function.py` which contains a couple of functions to fetch and save the data, `dag.py` which contains codes for airflow. I will also give a `Dockerfile` , in case you need this project to deploy.

1. codes for `function.py`
    

```python
# function to fetch the case data
def fetch_cases():
    # request to the API to get the case data
    response = requests.get('https://api.covid19api.com/dayone/country/india/status/confirmed')
    data = response.json()

    # Extract the relevant fields from the data
    cases = []
    for record in data:
        date = record['Date']
        cases = record['Cases']
        cases.append({'date': date, 'cases': cases})

    return cases


# Define a function to save the case data to BigQuery
def save_cases(**kwargs):
    # Extract the case data from the kwargs
    cases = kwargs['ti'].xcom_pull(task_ids='fetch_cases')

    # Create a BigQuery client
    client = bigquery.Client()

    # Create a new dataset
    dataset = bigquery.Dataset(client.dataset('covid_data_dataset'))
    dataset.location = 'US'
    dataset = client.create_dataset(dataset)

    # Create a new table in the dataset
    table = bigquery.Table(dataset.table('case_data_table'), schema=[
        bigquery.SchemaField('date', 'DATE'),
        bigquery.SchemaField('cases', 'INTEGER')
    ])
    table = client.create_table(table)

    # Load the data into the table
    errors = client.insert_rows(table, rows=cases)
    if errors:
        print(errors)
```

1. codes for `dag.py`
    

```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.utils.dates import days_ago
import requests
from datetime import timedelta
import json
from google.cloud import bigquery
from function import fetch_cases, save_cases

default_args = {
    'owner': 'my-covid-dag',
    'start_date': days_ago(2),
    'depends_on_past': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

dag = DAG(
    'covid_cases_fetch_push',
    default_args=default_args,
    description='Fetch daily COVID-19 case data and store it in BigQuery',
    schedule_interval='@daily',
)

fetch_cases_task = PythonOperator(
    task_id='fetch_cases',
    python_callable=fetch_cases,
    dag=dag,
)

save_cases_task = PythonOperator(
    task_id='save_cases',
    python_callable=save_cases,
    provide_context=True,
    dag=dag,
)


fetch_cases_task >> save_cases_task
```

1. codes for `Dckerfile`
    

```python
FROM python:3.10

RUN pip install requests
RUN pip install pip install python-csv

# Copy the code into the image
COPY covid_fetch.py .  # . means current directory, set yours.

# Set the working directory
WORKDIR .     # . means current directory, set yours.

CMD ["python", "covid_fetch.py"]
```

### Save to local

If you don't want to save the data into tables instead you want the data into `.csv` format saved directly into your local directory then just modify `function.py` by changing `save_cases` function with the below codes.

```python
# Define a function to save the case data to a CSV file
def save_cases(**kwargs):
    # Extract the case data from the kwargs
    cases = kwargs['ti'].xcom_pull(task_ids='fetch_cases')

    # Write the case data to a CSV file
    with open('./cases.csv', 'w', newline='') as csvfile:
        fieldnames = ['date', 'cases']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
        writer.writeheader()
        for case in cases:
            writer.writerow(case)
```