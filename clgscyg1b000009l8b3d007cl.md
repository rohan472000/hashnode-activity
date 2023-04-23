---
title: "Getting Started with Data Engineering: A Step-by-Step Guide"
datePublished: Sun Apr 23 2023 19:55:36 GMT+0000 (Coordinated Universal Time)
cuid: clgscyg1b000009l8b3d007cl
slug: getting-started-with-data-engineering-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/4-EeTnaC1S4/upload/51b5c11a511c26def7d2a31d79ada7ae.jpeg
tags: data, github, python, gcp, dataengineering

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682190610105/195b7998-831c-4bf8-a92e-d36a4851282a.png align="center")

Are you interested in becoming a data engineer but don't know where to start? In this post, I'll walk you through the basics of data engineering using a simple project that involves fetching data from GitHub and visualizing it through Looker.

### Steps:-

Here's what you need to do:

1. **<mark>Select a programming language:</mark>** Data engineering requires you to be proficient in at least one programming language. Python is a popular choice because it has a rich set of libraries that can be used for data manipulation, transformation, and analysis.
    
2. **<mark>Choose a cloud provider:</mark>** Several cloud providers offer data engineering services such as AWS, GCP, and Azure. For this project, we'll be using GCP because it provides an easy-to-use service called BigQuery for storing and analyzing large datasets.
    
3. **<mark>ETL:</mark>** ETL stands for extract, transform, and load. This is the process of taking data from one source, transforming it to meet your requirements, and loading it into a destination. In our project, we'll be using an API provided by GitHub to extract data about the top 200 repositories with the highest stars.
    
4. **<mark>Load data into BigQuery:</mark>** Once we have the data, we need to load it into BigQuery so that we can analyze it. We'll be using the BigQuery Python client library to do this.
    
5. **<mark>Visualize the data:</mark>** Finally, we'll be using Looker to visualize the data. Looker is a business intelligence tool that allows you to create interactive dashboards and reports.
    

But wait, there's more! To automate this process and make it repeatable, you'll need an orchestration tool like Apache Airflow or Apache NiFi to schedule and execute your data pipeline.

If you're interested in seeing the project in action, you can check it out here: [https://github.com/rohan472000/Github-repo-extraction-GCP](https://github.com/rohan472000/Github-repo-extraction-GCP)

Data engineering can seem overwhelming at first, but with a little bit of practice and patience, you'll be able to master it in no time. Good luck!