# Web Scrapping & Apache Airflow

[please check my previous blog on the installation of apache airflow](https://rohan-anand.hashnode.dev/apache-airflow-installation)

### Introduction

In this blog, I'm going to tell you how to schedule your project with Apache Airflow, so that you don't have to trigger your function/projects on your own, it will be taken care of by DAGs.

### Brief Introduction of Airflow and DAGs

<mark>Apache Airflow </mark> is used for the **scheduling and orchestration of data pipelines or workflows**. Orchestration of data pipelines refers to the sequencing, coordination, scheduling, and managing of complex data pipelines from diverse sources.

<mark>DAGs </mark> (Directed Acyclic Graphs) are a set of tasks to be executed at some interval as scheduled. It is a collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies.

### Codes

To follow the below codes, you need to check out my previous blog '[Web Scrapping demo project'](https://rohan-anand.hashnode.dev/web-scrapping-demo-project) as I will be taking reference of functions inside that project.

Below are the codes for DAGs...

```python
from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.python import PythonOperator
from web_scrap import web_scrap  # import function from previous project

default_args = {
    'owner': 'xyz-web-scrap',
    'depends_on_past': False,
    'start_date': datetime(2022, 12, 12),
    'email': 'xyz@gmail.com',
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 0,  # removing retries to not call insert duplicates into BigQuery
    'retry_delay': timedelta(minutes=5),
}
dag = DAG(
    dag_id='rohan-dag-astro',
    description='first project with astronomer platform',
    default_args=default_args,
    schedule_interval='* * * * *',
    tags=['data-pipeline-dag'],
    max_active_tasks=3
)

with dag:
    run_dag = PythonOperator(
        task_id='complete_web_scrap',
        python_callable=web_scrap,
        dag=dag,
    )

run_dag
```

If you want to insert an email notification in above codes so that you can get notifications then use the below codes...

```python
import smtplib
def send_mail():
    server = smtplib.SMTP_SSL('smtp.gmail.com',465)
    server.ehlo()
    #server.starttls()
    server.ehlo()
    server.login('xyz@gmail.com','xxxxxxxxxxxxx') # use temporary passwords from google passwords
    
    subject = "abcdef......."
    body = "Your words........."
    msg = f"Subject: {subject}\n\n{body}"
    print('This mail going to be sent')
    server.sendmail(
        'asdfgh@gmail.com',
        'bvcxz@gmail.com',
        msg
    )
    print('mail has sent')
    server.quit()
```