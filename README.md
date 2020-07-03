# Udacity Nano Degree Data Engineering Capstone Project - Purpose 
- As more and more immigrants move to the US, people want quick and reliable ways to access certain information that can help inform their immigration, such as weather of the destination, demographics of destination. And for regulators to keep track of immigrants and their immigration meta data such as visa type, visa expire date, entry method to the US.

- Using the available data sources listed above, we build a Data Lake available on S3 that can be used to query for weather and demographics of popular immigration destinations, which could be useful for both immigrants and regulators. Regulators can also access data about individual immigrants, date of arrival to the US, visa expiry dates and method of entries to improve decision making.

# Project Data Sources
- I94 Immigration Data: This data comes from the US National Tourism and Trade Office Source. 
- World temperature Data: This dataset comes from Kaggle Source. 
- US City Demographic Data: This dataset comes from OpenSoft Source.  

# ETL pipeline 1 - Preprocess the data (**Use Apache Spark to preprocess the data and store it into S3**)
This ETL pipeline preprocess the Project data sources(above) and load it into AWS S3.  This pipeline is implemented in **etl/s3_to_redshift_etl.py**

# ETL pipeline 2 - Load processed data to Data Warehouse (**Apache Airflow DAGs to transfer data from S3 to Redshift**)
The ETL pipeline should extract from S3, loads it into Redshift staging tables and then copy it to Redshift fact and dimension tables.To complete the project, we created custom Airflow operators to perform tasks such as staging the data, filling the data warehouse, and running data quality checks on the data as the final step.

# Project Files
## Data Engineer Capstone Project.ipynb - Notebook that explains the End-to-End flow of this Project
- **etl/s3_to_redshift_etl.py** -  Loads datasets to S3
- **airflow/dags/dag_capstone_s3_to_redshift.py** - Loads data from S3 to Redshift fact and dimension tables
- **airflow/plugins/operators/stage_redshift.py** - Loads data from S3 to Redshift fact and dimension tables
- **airflow/plugins/operators/data_quality.py** - Apply data quality checks on Redshift fact and dimension tables
- create_tables.sql - used to create fact and dimension tables

# Project Execution Instructions
- ETL pipeline 1 - **etl/s3_to_redshift_etl.py** cambe executed from unix console
- ETL pipeline 2 - The Airflow DAG and custom operators needs to downloaded form the **airflow** folder and placed into the corresponding folders inside your AIrflow installaiton. Then run the DAG **data_engineering_project**.
- Notes: 
-- After you have updated the DAG, you will need to run /opt/airflow/start.sh command to start the Airflow webserver. 
-- Add the AWS connection 'aws_credentials' from the Admin->Connections menu
-- Add the Redshift connection 'redshift' from the Admin->Connections menu

