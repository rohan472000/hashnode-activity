# Jovian

### Introduction

Jovian is a cloud platform for storing and managing Jupyter notebooks, code, and data.

To use Jovian, you will need to install the `jovian` Python library and authenticate your account using an API key.

Below is the process to do it.

### Process

1. Install the `jovian` library by running the following command in a cell:
    
    ```python
    >>> !pip install jovian --upgrade
    ```
    
2. Once the installation is complete, import the `jovian` library and call the `jovian.authenticate()` function, as follows:
    
    ```python
    >>> import jovian
    
    >>> jovian.authenticate()
    ```
    
    This will prompt you to enter your API key, which you can find in your Jovian account settings.
    
3. Once you have authenticated your account, you can use the `jovian` library to save and share your notebooks. For example, you can use the `jovian.commit()` function to save a snapshot of your notebook, as follows:
    
    ```python
    >>> jovian.commit(project='my_project_name')
    ```
    

This will create a new version of the notebook and save it to your Jovian account, along with any code and data files associated with the notebook. You can then use the Jovian platform to view and manage your saved notebooks, as well as share them with others.

### Google Colab Notebook

When I tried to do the above things in Google Colab then I got this result.....

```python
>>> jovian.commit(project='credit-card-India')

Output :- 
[jovian] Detected Colab notebook...
[jovian] jovian.commit() is no longer required on Google Colab. If you ran this notebook from Jovian, 
then just save this file in Colab using Ctrl+S/Cmd+S and it will be updated on Jovian. 
Also, you can also delete this cell, it's no longer necessary.
```

### Summary

You don't need Jovian in Google Colab, use it in Jupyter notebook or other notebooks.