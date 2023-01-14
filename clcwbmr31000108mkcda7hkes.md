# Limitations of 'Pandas'

### Introduction

Pandas is a popular and powerful library for data manipulation and analysis in Python. It provides easy-to-use data structures and data analysis tools for handling and manipulating numerical tables and time series data.

The two primary data structures in pandas are the Series (1-dimensional) and DataFrame (2-dimensional). The Series object is similar to a column in a spreadsheet or a one-dimensional array, while the DataFrame object is similar to a table in a relational database or a two-dimensional array.

Pandas provides a wide range of tools for data manipulation and analysis, including data filtering, aggregation, and transformation. It also provides functionality for handling missing data and working with time series data.

### Realizations

Recently, I came across a situation in an ongoing project where I had to look for an alternative to pandas, this happened when the data was 1 Petabyte and even more.

My approach was to convert the table data into pandas DataFrame and then start analyzing and further processing, but you can't just easily convert the petabyte data into DataFrame for further processing, it cost you time and even system crash, it is also not a good practice to use pandas for a huge dataset.

### Limitations

Pandas is a popular and powerful library for data manipulation and analysis in Python. However, it has some limitations when dealing with very large datasets. Some of these limitations include:

* Memory limitations: Pandas stores data in memory and can consume a lot of memory when working with large datasets. This can cause performance issues and even crash the program.
    
* Slow performance: Pandas can be slow when performing certain operations on large datasets, especially when working with data that does not fit in memory.
    
* Limited support for distributed computing: Pandas is not designed for distributed computing and does not have built-in support for working with data that is spread across multiple machines.
    

### Alternatives

Note:- If possible then try to use SQL queries(static or dynamic) for dealing with large datasets in a table before going for the below alternatives.

Alternatives to Pandas for working with large datasets include:

* Dask: Dask is a parallel computing library that can be used to work with large datasets that do not fit in memory. It allows you to perform operations on data in a distributed environment, which can be faster and more memory-efficient than using Pandas alone.
    
* Apache Arrow: Apache Arrow is a columnar in-memory data format that is designed to work with large datasets. It can be used with a variety of libraries, including Pandas, to improve performance when working with large datasets.
    
* Vaex: Vaex is a python library that allows you to perform out-of-core (data is read from disk as needed) and lazy computations on large datasets. This allows you to work with datasets that are much larger than the available memory.
    
* PySpark : PySpark is a python library that allows you to perform distributed data processing using the Apache Spark framework. PySpark allows you to work with large datasets in a distributed computing environment, making it a good alternative for data processing and analysis at scale.