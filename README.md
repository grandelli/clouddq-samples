# CloudDQ Demos
## Context
[CloudDQ](https://github.com/GoogleCloudPlatform/cloud-data-quality) is an open source cloud-native, declarative, and scalable Data Quality validation Command-Line Interface (CLI) application for Google BigQuery. CloudDQ allows users to define and schedule custom Data Quality checks across their BigQuery tables. Data Quality validation results will be available in another BigQuery table of their choice. Users can then build dashboards or consume data quality outputs programmatically and monitor data quality from the dashboards and data pipelines.

CloudDQ is also the data quality engine running under the hood of Google Cloud [Dataplex](https://cloud.google.com/dataplex), which allows to create and maintain CloudDQ tasks with very low effort (within Dataplex, tasks are also known as **DQ Tasks**). Among the main benefits of preferring DQ Tasks over OSS CloudDQ:
* Dataplex is a managed service and it does not require any explicit CloudDQ setup or configuration
* Within Dataplex, CloudDQ routines are executed on [Serverless Spark](https://cloud.google.com/solutions/spark), with high scalability and no need to setup a dedicated infrastructure
* DQ Tasks is based on a CloudDQ version actively supported by Google Cloud, while the OSS CloudDQ is not
* For customers already using the OSS Cloud DQ, the migration effort is very low, since the syntax is almost the same and Dataplex adds some benefits, by automating some repetitive steps

## Goal
This repository contains common samples of CloudDQ routines, both for the OSS CloudDQ and [DQ Tasks](https://cloud.google.com/dataplex/docs/data-quality-overview).

## Project Setup
In the repo you can find a sample dataset. All the samples refer to this data:

* Open a CLI in a virtual machine (e.g. Cloud Shell CLI) and run the following commands (**heads-up** replace the angular brackets with your own parameters):

        export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value project)
        export CLOUDDQ_BIGQUERY_REGION=EU
        export CLOUDDQ_BIGQUERY_DATASET=clouddq_dataset
        export CLOUDDQ_TARGET_BIGQUERY_TABLE="<gcp-project-id>.clouddq_dataset.data_output"
* \[Only Once\] If not existing, create the dataset:

        bq --location=${CLOUDDQ_BIGQUERY_REGION} mk --dataset ${GOOGLE_CLOUD_PROJECT}:${CLOUDDQ_BIGQUERY_DATASET}

### Metric dataset loading
    bq load --source_format=CSV --replace --autodetect ${CLOUDDQ_BIGQUERY_DATASET}.metrics metrics.csv

### Inventory loading
    bq load --source_format=CSV --replace --autodetect ${CLOUDDQ_BIGQUERY_DATASET}.inventory inventory.csv
