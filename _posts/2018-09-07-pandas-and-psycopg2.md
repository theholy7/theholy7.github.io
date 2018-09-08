---
layout: post
title: Use psycopg2 to query into a DataFrame
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - Python
  - Pandas
  - pycopg2
  - PostgreSQL
---
I love working with Python + Pandas, but sometimes working with lots of data or even loading
that data into memory can be a problem.

It can be better to have a database to perform DB operations, like merges and filters, and then
do the final operations in Pandas, when the data is more manageable. For that I use Postgres + Python,
with `psycopg2` before loading the data into Pandas. Lets get to work!<!--more-->

I like to start by loading my database variables into memory using `python-dotenv`. Here's how:
* Create a `.env` file with

```bash
SQL_USER='your_user'
SQL_PASS='your_pass'
SQL_HOST='your_localhost'
SQL_PORT='your_port'
SQL_DB='your_db'
```
* Load that file into your `.py` or your `.ipynb` file

```python
import os
from dotenv import load_dotenv, find_dotenv

load_dotenv(find_dotenv())

SQL_USER = os.environ.get('SQL_USER')
SQL_PASS = os.environ.get('SQL_PASS')
SQL_HOST = os.environ.get('SQL_HOST')
SQL_PORT = os.environ.get('SQL_PORT')
SQL_DB = os.environ.get('SQL_DB')
```

Then you can use these variables to connect to your database:
```python
import psycopg2

conn = psycopg2.connect(
    dbname=SQL_DB,
    user=SQL_USER,
    password=SQL_PASS,
    port=SQL_PORT,
    host=SQL_HOST
)

```
If everything went fine so far, you won't see any error messages. The next step is to build the query we want to pass to
the database, and execute it. We can pass normal SQL queries and execute them with `pscycopg2` and then we can as a final
step load that data into `Pandas`. Here is the code:
```python
import pandas.io.sql as sqlio

SQL_QUERY = "SELECT * FROM test_table WHERE id = ANY(%s)"
test_ids = [1, 2, 3]

result_df = sqlio.read_sql_query(SQL_QUERY, params=(test_ids,), conn)
```

And boom! The results of your query show up in a dataframe. You can get all the [code here](https://gist.github.com/theholy7/bd3916f370747d781410772c8ae783e1)
if you want to star my gist, or copy paste from below.
<script src="https://gist.github.com/theholy7/bd3916f370747d781410772c8ae783e1.js"></script>
Best, Jose :)
