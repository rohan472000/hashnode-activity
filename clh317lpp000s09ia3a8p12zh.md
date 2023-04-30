---
title: "Automatically Document Your Database in Markdown"
datePublished: Sun Apr 30 2023 06:29:38 GMT+0000 (Coordinated Universal Time)
cuid: clh317lpp000s09ia3a8p12zh
slug: automatically-document-your-database-in-markdown
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/0DJHJcpwN9Q/upload/19915892fb996e17330a0a0ad3da3fc7.jpeg
tags: python, mysql, markdown, databases, script

---

If you're working with databases, you know how important it is to keep track of the schema and column information for each table. One way to do this is to manually create documentation in a format like Markdown, but that can be time-consuming and error-prone. Fortunately, with a few lines of code in Python and MySQL, you can automatically generate Markdown documentation for your database tables.

## **How it Works**

The Python script connects to a MySQL database and queries the schema to get a list of all the tables. It then loops through each table, retrieves the column information, and generates a Markdown table with the column names, types, nullability, key constraints, default values, and any extra information.

The script then writes the Markdown table to a separate file for each table, with the filename matching the table name. By default, the script overwrites any existing files with the same name, but you can modify the code to append the Markdown table to the file instead.

## **Scripts**

```python
import mysql.connector
from mysql.connector import errorcode

# Config file
config = {
    'user': 'root',
    'password': 'rohan',
    'host': 'localhost', # specify port if needed
    'database': 'sakila' # database name which exist under you DB
}

# Database Connection
try:
    cnx = mysql.connector.connect(**config)
    cursor = cnx.cursor()
    print("Connection Successful")
except mysql.connector.Error as err:
    if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
        print("Something is wrong with your user name or password")
    elif err.errno == errorcode.ER_BAD_DB_ERROR:
        print("Database does not exist")
    else:
        print(err)

# Query the database schema
cursor.execute("SHOW TABLES")
tables = cursor.fetchall()

# Generate Markdown documentation for each table
for table in tables:
    table_name = table[0]
    cursor.execute(f"DESCRIBE {table_name}")
    columns = cursor.fetchall()

    # Create a Markdown table with column information (check /n and \n)
    table_md = f"## Table {table_name}\n\n"
    table_md += "| Column | Type | Null | Key | Default | Extra |\n"
    table_md += "| ------ | ---- | ---- | --- | ------- | ----- |\n"

    for column in columns:
        column_md = "| " + " | ".join(str(x) for x in column) + " |\n"
        table_md += column_md

    # Append the Markdown document to the file, if you don't need to give description, then you can comment out last 6 lines in below code block.
    with open(f"{table_name}.md", "a") as f:
        f.write(table_md)
        
        # Prompt the user for a table description and append it to the file
        description = input(f"Enter a description for {table_name}: ")
        f.write(f"\n{description}\n")

        # Print the contents of the file
        f.seek(0)
        print(f.read())

    # # Print the contents of the file
    # with open(f"{table_name}.md", "r") as f:
    #     print(f.read())

# Close the DB connection
cursor.close()
cnx.close()
```

The script then prompts the user to input a description for each table and appends it to the end of the Markdown file for that table. The `with open(f"{table_name}.md", "a") as f` block opens the Markdown file in "a" (append) mode, allowing the `f.write(table_md)` statement to append the Markdown document to the file instead of overwriting it. After appending the Markdown document and the user-provided description, the script reads the contents of the file and prints it to the console using [`f.seek`](http://f.seek)`(0)` and `print(`[`f.read`](http://f.read)`())`.

## **Usage**

To use the script, you'll need to have Python and MySQL installed on your machine and have the necessary credentials and permissions to connect to your database. You'll also need to modify the `config` dictionary at the beginning of the script to match your database connection details.

Once you've set up the script, simply run it from your terminal or IDE of your choice. It will generate a separate Markdown file for each table in your database, with the column information formatted as a Markdown table.

## **Conclusion**

Automatically generating Markdown documentation for your database can save you time and reduce the risk of errors in your documentation. With the Python and MySQL script provided above, you can easily generate Markdown tables for all the tables in your database, making it easier to keep track of your schema and column information. Give it a try and see how it can improve your workflow!