# DataPipeline-ETL-
ETL stands for Extract, Transform, Load. ETL is a type of data integration that extracts data from one or more sources (API, a database or a file), transforms it to match the destination system’s requirements and loads it into the destination system. 

Why ETL Pipeline?

Analytics, decision support systems, and operational reports rely on data. These are crucial for business, although we can run analytics against our source system, however, source systems are seldom optimized for querying. Extra analytics workload will slow down your business facing application. ETL comes into the picture here to move data from the source, transform it and load it to an optimized database/storage layer for data analytics. I will focus on Extract and Load components of ETL.
Building ETL Pipeline

There are many different tools and technologies we can use to build an ETL pipeline. Which you specifically need depends on your requirements and skillset. We will use Python and specifically Pandas and SQLAlchemy to extract and load data.

The Setup

I have prepared SQL Server and PostgreSQL environments which will serve as source and the destination environments respectively. We will use SQL Server’s AdventureWorks database as a source and load data in PostgreSQL with Python. Be sure to check out both videos if you want to follow along. I will perform some basic setup on the database side before writing the ETL pipeline. Following SQL scripts are available on GitHub. I will execute few queries in pgAdmin4.

First, I will create a database to house the incoming tables and data.
![image](https://github.com/user-attachments/assets/3178d9b0-925d-4eb7-aae3-eb38fb538f78)

Second, I will create a user and grant it connect permissions along with select, insert, update and delete. I will go ahead and create the same user in SQL Server environment to keep things consistent.

![image](https://github.com/user-attachments/assets/e93105ae-819b-4d09-9dc8-74dad3ee6237)

Third, I will save the credentials in environment variables. It’s a good habit to store your credentials separately. The goal is to protect the credentials from being exposed in the ETL script. You can use a configuration file or system environment variables.


The Extract

We need a strategy to plan our ETL pipeline. Usually, we map each table from the source to destination environment. Create similar objects with matching data types in both environments. We connect to both environments and perform mapping for each table and then trigger the pipeline. That sounds like a lot of work! Don’t worry we won’t be going through all that trouble. I want to showcase the versatility of Python and Pandas and how simple they can make this process. I will grab the tables I want to extract data from SQL Server’s system schema. Simply loop through the tables and query them. With a few lines of codes, we queried the source and obtained data as Pandas dataframe.

The Load

Pandas makes it a breeze to load data into a SQL database with pandas “to_sql()” function. As we loop through and query each table in the Extract, we call the next function defined as the load. We will follow the truncate and load approach as it is simple and it replace the tables with each run. This can be your staging environment where you pull in new data on a given interval. From here you can transform and load the data into the presentation layer. The code below demonstrates how to connect and store data in a PostgreSQL database using Pandas.
