<a href="https://github.com/Anmol-Baranwal/GIFs-For-Readme"><img src="https://forthebadge.com/images/badges/built-with-love.svg" width="130" alt="made with love  markdown badge" ></a>  <a href="https://github.com/Anmol-Baranwal/GIFs-For-Readme">

# APMorgan_data
APMorgan Data Engineering Project

## Project Goals

1. Data Ingestion: We need to build a proper mechanism to ingest data from various application sources into ADLS GEN2.
2. ETL System: We always get the data in raw format, so we must transform this data into usable format by using required transformations in Azure Data Factory.
3. Data lake: We get data from different sources so we need to have a centralized repo to store them. Here we are using ADLS Gen 2.
4. Scalability: You never know when we are going to get huge volumes of data, so we need to make sure that our system is able to cope up with that sudden change.
5. Cloud: When we have vast data it is always better to go with cloud because it is easy to use and scalable. Here we are using Azure cloud environment.
6. Azure DataBricks: When data is huge the first thing that should come into your mind is Azure DataBricks which is fast and can deal with huge volumes of data.

## Services that we are going to use in this project.

1. Azure Data Lake Stoage Gen 2 : It is a scalable and secure cloud-based storage service provided by Microsoft Azure. It is designed to store and manage big data in its native format.
2. Azure DataBricks : It is a cloud-based analytics platform developed in collaboration with Databricks. It offers a fast, collaborative, and scalable environment for big data analytics and machine learning.
3. Azure Data Factory : It is a cloud-based data integration service and it enables users to efficiently orchestrate and automate the movement and transformation of data between different data stores and systems.
4. Azure SQL server : it is a fully managed relational database service and it is built on the same SQL Server engine, offering all the features and capabilities of SQL Server with the added benefits of cloud scalability, high availability, and automated management.
5. Azure Triggers : These are specifically Azure Functions Triggers, are event-driven mechanisms in the Azure cloud platform. They allow users to execute serverless functions in response to specific events or triggers like data changes.
6. Azure Key Vault : It allows users to securely store and manage cryptographic keys, secrets, and certificates used by cloud applications and service and we can place strict access control restrictions to make sure data is safe.
7. SSMS : It is a comprehensive and user-friendly integrated development environment (IDE) provided by Microsoft for managing and interacting with Microsoft SQL Server.

## Architecture Used

<img width="394" alt="APMorgan_Archiecture" src="https://github.com/venkat2705/APMorgan_data/assets/60357150/f1d0762c-cf9b-45c5-a928-3a9656bbe7a7">


## High Level Project Flow

Data comes to ADLS Landing Folder --> Goes through ADF Pipeline --> DataBricks (schema evaluation through SQL Database Schema) --> Secrets stored in Azure Key Vault --> Staging or Rejected.

## Detailed Proejct Flow

1. Ingest data into landing folder in ADLS input container. This is the source side of the ADF pipeline.
2. Now coming to the destination side of the ADF pipeline we need to setup a Databricks file. For that we must set up DataBricks account and then import the attched project (python) file.
3. It's time to evaluate the data in Databricks. We have two main things to focus on, Duplicate rows and Date Schema validation. For date schema evaluation we need to set up SQL database(create tables using given SQL script) and import the schema to data bricks for incoming data evaluation.
4. Lets create a Key Vault to store all the sensitive information like passwords and tokens.
5. We need to give required IAM access(like Key Vault Administrator, Key Vault Certificates Officer...etc) in KeyVault to the user to access the secrets from different Azure services.
6. Final step it to create an ADF pipeline and mount data from ADLS to Databricks to perform necessary validations to segregate data into Staging and rejected folders.
7. Now put a storage event trigger. So, when the data is ingested into the landing folder then the trigger automatically triggers the pipeline and data bricks evaluates data. Data will be stored in eligible folder (either staging or Rejected).
8. Now the data is enriched and available for the downstream departments.

You need to have good knowledge on Azure cloud services especially Azure Data factory, Azure SQL server, Azure databricks, Azure Key Vault to be able to perform the required ETL operations and analytics in SQL. Must be able to allow necessary permissions on the fly as required.

