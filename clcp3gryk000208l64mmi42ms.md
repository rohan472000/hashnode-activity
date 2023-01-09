# NASDAQ data pipeline through GCP

### Introduction

This blog gives a brief knowledge of how a pipeline is made and works to fetch, and analyze it further as per requirement, I will be doing this by taking GCP into account.

### Pre-requisites

`google-cloud` library should be installed by using `pip install google-cloud` and you should have a GCP account with admin access(to avoid any restrictions) or a service account with required privileges.

You should have a project(project\_id needed), a BigQuery table, and PubSub(topic).

### Procedure

1. Import all necessary libraries
    

```python
import requests
import logging
import os

from google.cloud import pubsub_v1
from google.cloud import bigquery
```

1. We need to keep logs of every activity.
    

```python
logging.basicConfig()
logger = logging.getLogger()
logger.setLevel(logging.INFO)
```

1. We will store data in BigQuery tables, and for that, set up a BigQuery client.
    

```python
bigquery_client = bigquery.Client()
```

1. We need to define a function to process the incoming data
    

```python
def process_data(data, context):
    data = json.loads(data)  # parse the incoming data
    # insert the data into BigQuery table
    table_id = os.environ['BIGQUERY_TABLE_ID']
    table = bigquery_client.get_table(table_id)
    row_to_insert = [data]
    errors = bigquery_client.insert_rows(table, row_to_insert)
    if errors == []:
        logger.info('New row added to {}'.format(table_id))
    else:
        logger.error('Errors: {}'.format(errors))
```

1. Setup PubSub client
    

```python
publisher = pubsub_v1.PublisherClient()
topic_name = 'projects/{project_id}/topics/{topic}'.format(
    project_id=os.environ['GOOGLE_CLOUD_PROJECT'],
    topic=os.environ['PUBSUB_TOPIC'])
# set topic in the Cloud Function's environment variables
```

1. Now, define your cloud function
    

```python
def pubsub_to_bigquery(event, context):
    logger.info("Event: " + str(event))
    data = base64.b64decode(event['data']).decode('utf-8')
    process_data(data, context)
```

1. Last, define a function to fetch Nasdaq data
    

```python
def fetch_nasdaq_data():
    response = requests.get('https://api.nasdaq.com/api/quote/AAPL/info?assetclass=stocks')
    data = response.json() 

    # publish the data to the Cloud Pub/Sub topic
    publisher.publish(topic_name, data=json.dumps(data).encode('utf-8'))

# fetch nasdaq data function on a regular interval
while True:
    fetch_nasdaq_data()
    time.sleep(60)  # fetching data every 60 seconds
```