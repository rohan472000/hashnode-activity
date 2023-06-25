---
title: "Difference Between Reschedule Mode and Deferrable Flag in Airflow Sensors"
datePublished: Sun Jun 25 2023 15:05:24 GMT+0000 (Coordinated Universal Time)
cuid: cljbkakxj000t09l2hzrjhie0
slug: difference-between-reschedule-mode-and-deferrable-flag-in-airflow-sensors
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687705438018/dd8773a4-8925-4fbc-8bed-3592fea3f981.png
tags: github, python, opensource, apache, airflow

---

### Motivation

Recently my PR for adding the `difference between Deferrable and Non-Deferrable Operators` got merged in `apache-airflow`, you can see it here - [PR Link](https://github.com/apache/airflow/pull/31840). So I thought to explain it through a blog.

### Introduction

Airflow sensors are a special kind of operator that is designed to wait for something to happen. When sensors run, they check to see if a certain condition is met before they are marked successful and let their downstream tasks execute. There are two modes available in Airflow sensors, "poke" and "reschedule". In this blog, we will discuss the difference between the "reschedule" mode and the "deferrable" flag in sensors.

### Reschedule Mode

* When the sensor mode is set to "reschedule", if the criteria are not met, then the sensor releases its worker slot and reschedules the next check for a later time.
    
* This mode is best if you expect a long runtime for the sensor because it is less resource-intensive and frees up workers for other tasks.
    
* Between each wait\_interval, when the sensor is not checking your criteria anymore, the slot is released, and your sensor gets the status "up\_for\_reschedule". Meanwhile, your other tasks can run.
    
* "up\_for\_reschedule" means your sensor is going to be rescheduled at a later time, or more specifically at the `current date + wait_interval`.
    

### Deferrable Flag

* The "deferrable" flag is used to mark a task as deferrable, which means that it can be deferred to a later time if it fails to run.
    
* When a task is marked as deferrable, it is put in a "up\_for\_reschedule" state if it fails to run.
    
* The task is then rescheduled for a later time, or more specifically at the `current date + wait_interval`.
    
* The "deferrable" flag is not a common behavior in sensors, and it is only used in a few of them.
    

### Which mode should you use?

* If the expected runtime of your sensor is short or if the wait\_interval is short like less than a minute, go with the "poke" mode.
    
* If the expected runtime is quite long, then go with the "reschedule" mode.
    

### Code snippet to understand better

Below is the example code snippet that demonstrates the difference between the "reschedule" mode and the "deferrable" flag in sensors:

```python
from airflow import DAG
from airflow.operators.sensors import FileSensor
from datetime import datetime, timedelta

default_args = {
    'owner': 'rohan',
    'depends_on_past': False,
    'start_date': datetime(2023, 5, 24),
    'email_on_failure': 'xcv@gmail.com',
    'retries': 1,
    'retry_delay': timedelta(minutes=2),
}

dag = DAG(
    'my-example-dag',
    default_args=default_args,
    schedule_interval=timedelta('5 4 * * *'),
)

# Reschedule mode
waiting_for_file_reschedule = FileSensor(
    task_id='reschedule_task',
    poke_interval=120,
    timeout=800,
    mode="reschedule",
    dag=dag,
)

# Deferrable flag
waiting_for_file_deferrable = FileSensor(
    task_id='deferrable_task',
    poke_interval=120,
    timeout=800,
    deferrable=True,
    dag=dag,
)
```

In this example, we have two sensors, one with the "reschedule" mode and one with the "deferrable" flag. The `FileSensor` operator waits for a file to appear in a specified directory before it is marked successful and lets its downstream tasks execute.

The `waiting_for_file_reschedule` sensor uses the "reschedule" mode, which means that if the criteria are not met, then the sensor releases its worker slot and reschedules the next check for a later time. This mode is best if you expect a long runtime for the sensor because it is less resource-intensive and frees up workers for other tasks.

The `waiting_for_file_deferrable` sensor uses the "deferrable" flag, which means that if the task fails to run, it is put in a `up_for_reschedule` state and rescheduled for a later time. The "deferrable" flag is only used in a few sensors.

### Conclusion

It's worth noting that bugs and errors in the sensors may be masked by timeouts, which however may be mitigated by properly written unit tests. Some overhead is added to the scheduler, as such polling intervals may not be too frequent, and a separate process is spawned. In conclusion, the "reschedule" mode and the "deferrable" flag in sensors are used to free up resources and reschedule tasks for a later time if they fail to run. The "reschedule" mode is best for long-running sensors, while the "deferrable" flag is only used in a few sensors. It's important to choose the appropriate mode based on the expected runtime of your sensor and the wait\_interval