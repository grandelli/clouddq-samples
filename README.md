# CloudDQ Demos
This repo contains data quality checks for Google CloudDQ. 

## Project Setup / Dataset Upload

* Follow the instructions to install CloudDQ in a VM (e.g. GCP Cloud Shell)
* Copy the *configs* folders within the root folder of your CloudDQ executable
* Open a terminal in the VM and run the following commands (**heads-up** insert your own parameters)

export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value project)
export CLOUDDQ_BIGQUERY_REGION=EU
export CLOUDDQ_BIGQUERY_DATASET=<bq-dataset-name>
export CLOUDDQ_TARGET_BIGQUERY_TABLE="<gcp-project-id>.<bq-dataset-name>.data_output"
bq --location=${CLOUDDQ_BIGQUERY_REGION} mk --dataset ${GOOGLE_CLOUD_PROJECT}:${CLOUDDQ_BIGQUERY_DATASET}

### Metric dataset loading
bq load --source_format=CSV --replace --autodetect ${CLOUDDQ_BIGQUERY_DATASET}.metrics metrics.csv

### Inventory loading
bq load --source_format=CSV --replace --autodetect ${CLOUDDQ_BIGQUERY_DATASET}.inventory inventory.csv

## CloudDQ Examples
### Count
python3 clouddq_executable.zip \
    DQ_COUNT \
    configs \
    --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
    --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
    --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
    --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Nullability Controls
#### Missing values in columns
python3 clouddq_executable.zip \
   DQ_NODE_ACCOUNT_VALUE_NOT_NULL,DQ_KPI_VALUE_VALUE_NOT_NULL \
    configs \
    --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
    --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
    --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
    --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Duplicates
python3 clouddq_executable.zip \
    DQ_KPI_DUPLICATE \
    configs \
    --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
    --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
    --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
    --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Presence of Keys
#### Foreign Key Enforcement
python3 clouddq_executable.zip \
    DQ_FOREIGN_KEY_VALID \
    configs \
    --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
    --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
    --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
    --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"
