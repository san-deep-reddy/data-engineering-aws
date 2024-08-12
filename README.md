# Automated Real Estate Data Pipeline in AWS

## Zillow Real Estate Data Pipeline 

This repository contains the code for a data pipeline that extracts real estate data from the Zillow Rapid API, transforms it, and loads it into a Redshift data warehouse. The pipeline is orchestrated using Airflow.

### Project Overview

This project demonstrates how to build an end-to-end data pipeline using Python, AWS S3, AWS Lambda, and Airflow. The pipeline performs the following tasks:

1. **Extract:** Fetches real estate data for a specific location from the Zillow Rapid API.
2. **Transform:** Converts the extracted JSON data into a CSV format. 
3. **Load:** Uploads the transformed data (CSV) to an S3 bucket.
4. **Load (Redshift):** Loads the data from S3 into a Redshift data warehouse table for further analysis.

### Code Breakdown

The project consists of three main components:

  * **Lambda functions:**
      * `copyRawJsonFile-lambdaFunction.py`: Copies a raw JSON file downloaded from the Zillow API to another S3 bucket.
      * `transformation-convert-to-csv-lambdaFunction.py`: Downloads a JSON file from S3, transforms it into a CSV format by selecting specific columns, and uploads the resulting CSV file to another S3 bucket.
  * **Airflow DAG:**
      * `zillowanalytics.py`: Defines an Airflow DAG that orchestrates the data pipeline tasks. It calls the Python function to extract data from the Zillow API, uses a Bash Operator to copy the downloaded file to S3, waits for the file to be available using an S3KeySensor, and finally utilizes the S3ToRedshiftOperator to load the data into the Redshift data warehouse.

### Requirements

* Python 3.x
* boto3 library
* pandas library
* airflow
* AWS account with S3, Lambda, and Redshift services configured

### Setup

1. Install required libraries:
  ```bash
  pip install boto3 pandas airflow
  ```
2. Configure your AWS credentials and API keys.
3. Update the configuration details in `zillowanalytics.py` such as S3 bucket names, Redshift connection details, and Zillow API credentials.

### Usage

1. Run Airflow webserver and scheduler.
2. The Airflow DAG is scheduled to run daily (`@daily`) and will automatically trigger the data pipeline.

### Additional Notes

* The videos referenced in the prompt provided a high-level overview of the data pipeline. This code provides the specific implementation details. 
* Airflow is used to automate and schedule the data processing tasks.

This is a basic example, and you can extend it further by:

* Adding error handling and logging.
* Implementing unit tests. 
* Expanding the data transformation logic to include additional processing steps.

