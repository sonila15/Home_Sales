# Home_Sales
## SparkSQL Home Sales Analysis
This repository contains a Python script that performs analysis on home sales data using SparkSQL. The script reads in a CSV file from an AWS S3 bucket, creates a Spark DataFrame, and performs various queries on the data. It also demonstrates the use of caching and partitioning in Spark.

## Requirements
Spark 3.4.0
Java 11

## Installation
To run the script, follow these steps:

- Find the latest version of Spark 3.x from http://www.apache.org/dist/spark/ and set spark_version variable in the script to the appropriate version.
spark_version = 'spark-3.4.0'

- Install Spark and Java using the provided commands:
!apt-get update
!apt-get install openjdk-11-jdk-headless -qq > /dev/null
!wget -q http://www.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop3.tgz
!tar xf $SPARK_VERSION-bin-hadoop3.tgz
!pip install -q findspark

- Set the environment variables:
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-11-openjdk-amd64"
os.environ["SPARK_HOME"] = f"/content/{spark_version}-bin-hadoop3"

- Start a SparkSession:
from pyspark.sql import SparkSession
import findspark
findspark.init()
spark = SparkSession.builder.appName("SparkSQL").getOrCreate()

- Read in the AWS S3 bucket data into a DataFrame:
from pyspark import SparkFiles
url = "https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv"
spark.sparkContext.addFile(url)
df = spark.read.csv(SparkFiles.get("home_sales_revised.csv"), header=True, inferSchema=True)

- Perform the desired queries on the data using SparkSQL. Examples of queries are provided in the script.

- Run the script and observe the query results.

## Queries
The script demonstrates the following queries on the home sales data:

Average price for a four-bedroom house sold in each year rounded to two decimal places.
Average price of a home for each year the home was built that has 3 bedrooms and 3 bathrooms rounded to two decimal places.
Average price of a home for each year built that has 3 bedrooms, 3 bathrooms, two floors, and is greater than or equal to 2,000 square feet rounded to two decimal places.
"View" rating for the average price of a home, rounded to two decimal places, where the homes are greater than or equal to $350,000. The runtime for this query is also measured.
Cache the temporary table home_sales and check if it is cached.
Repeat the query from step 4 using the cached data and compare the runtime with the uncached runtime.
Partition the data by the date_built field on the formatted parquet home sales data.
Read the parquet formatted data.
## Conclusion
This script showcases how to perform various queries on home sales data using SparkSQL. It also demonstrates the use of caching and partitioning to improve query performance. Feel free to modify and expand upon the provided script for your own analysis.

Note: Make sure to have the necessary Spark and Java installations in place before running the script.





