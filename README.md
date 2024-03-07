# python-Athena

## Objectives of this repository
Detail and share how to use python scripts to connect to Amazon Athena, query the data and further leverage it in dataframes and other python scripts for data analysis.

## Context
For a professional project in which I had to generate demo data for our pre sales demo environment, it was clear that I needed to read data within our demo datamart to use it to create other objects and elements of the demo environment.\
We use AWS Athena, a service that allows to build databases on data files stored on AWS S3 buckets and to write standard SQL queries to retrieve data from those flat files.\
Therefore I needed to learn how to connect to and query Amazon Athena through my python scripts.\
More details below.

## Installation
The first step is to install the right libraries
> [!TIP]
> There are several methods to create a python wrapper to connect and query Athena databases.\
> The following article, [Connecting to AWS Athena databases using Python](https://medium.com/codex/connecting-to-aws-athena-databases-using-python-4a9194427638), is very helpful.\
> I decided to go with `PyAthena + SQLAlchemy` because it felt more natural to me but it seems according to the article that Boto3 offers better performances. I'll give it a try another time.

We use the following code to install the libraries:
```
pip install "SQLAlchemy>=1.0.0"
pip install PyAthena
```
> [!NOTE]
> We may need to restart the kernel to use updated packages.

## Create the connection
In order to query the tables in Athena we first need to have a connection setup and ready to use. 
```
from sqlalchemy import func, select
from sqlalchemy.engine import create_engine
from sqlalchemy.sql.schema import Table, MetaData

conn_str = "awsathena+rest://{aws_access_key_id}:{aws_secret_access_key}@athena.{region_name}.amazonaws.com:443/"\
           "{schema_name}?s3_staging_dir={s3_staging_dir}"

engine = create_engine(conn_str.format(
    aws_access_key_id="[we enter our access key here]",
    aws_secret_access_key="[we enter our secret key here]",
    region_name="[we enter the AWS server region here - east1, west2, etc ...]",
    schema_name="[we enter our database schema here]",
    s3_staging_dir="[we enter our S3 bucket here - s3://our_bucket/"]
))
```
  
## Query the data
Everything is ready for us to query the data. We will leverage the `pandas` library to use the `read_sql` function and put the results of our SQL query into a DataFrame.\
Example of a query to get the all data from the events table. We put them into a DataFrame called `events_df`\
```
import pandas as pd

events_df = pd.read_sql("SELECT * FROM events", engine)
events_df
```
