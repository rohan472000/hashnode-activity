# Web Scrapping using Python

### Introduction

Web scraping is an automatic method to obtain large amounts of data from websites. Generally, web scrapping is used to obtain large amounts of data to train models in Machine Learning. There are many different ways to perform web scraping to obtain data from websites. These include using online services, particular APIs or even creating your code for web scraping from scratch.

### Languages for Web Scrapping

Following are some popular languages for web scrapping:-

*   <mark>Python </mark> (most recommended)
    
*   Javascript
    
*   Java
    
*   C++
    

### Libraries used for Web Scrapping using <mark>python</mark>

*   BeautifulSoup
    
    ```python
    >>> from bs4 import BeautifulSoup
    >>> url = 'https://hashnode.com/'
    >>> page = requests.get(URL, headers=headers)
    >>> soup = BeautifulSoup(page.content, "html.parser")
    ```
    
*   Scrapy
    
    ```python
    >>> import scrapy
    ```
    
*   Selenium
    
    ```python
    >>> from selenium import webdriver
    >>> from selenium.webdriver.common.by import By
    >>> from selenium.webdriver.common.keys import Keys
    ```
    
*   Requests
    
    ```python
    >>> import requests
    >>> url = 'https://hashnode.com/'
    >>> r = requests.get(url)
    ```
    
*   Urlib3
    
    ```python
    >>> import urllib3
    >>> http = urllib3.PoolManager()
    >>> r = http.request('GET', 'http://httpbin.org/robots.txt')
    >>> r.status
    200
    >>> r.data
    'User-agent: *\nDisallow: /deny\n'
    ```
    
*   Lxml
    
    ```python
    >>> from lxml import etree as et
    >>> root = et.Element('html', version="5.0")
        et.SubElement(root, 'head')
        et.SubElement(root, 'title', bgcolor="red", fontsize='22')
        et.SubElement(root, 'body', fontsize="15")
    >>> print (et.tostring(root, pretty_print=True).decode("utf-8"))
    ```
    
*   Mechanical Soup
    
    ```python
    >>> import mechanicalsoup
    >>> browser = mechanicalsoup.StatefulBrowser()
    >>> browser.open("http://hashnode.com")
    ```