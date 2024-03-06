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

Use the following code to install the libraries
```
pip install "SQLAlchemy>=1.0.0"
pip install PyAthena
```


