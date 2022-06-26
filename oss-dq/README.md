# OSS CloudDQ
This repo contains data quality checks for the open source [CloudDQ](https://github.com/GoogleCloudPlatform/cloud-data-quality) engine. Be aware that the following does not apply to Dataplex DQ Tasks (refer to the corresponding section for this).

## CloudDQ Setup

* Follow the [instructions](https://github.com/GoogleCloudPlatform/cloud-data-quality/blob/main/USERMANUAL.md) to install CloudDQ in a virtual machine (e.g. GCP Cloud Shell CLI)
* Copy the *oss-dq* folder (containing entities, rule bindings and rules) within the root folder of your CloudDQ deployment. 
* Set the following variables in the shell (**heads-up** replace the angular brackets with your own parameters):

        export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value project)
        export CLOUDDQ_BIGQUERY_REGION=EU
        export CLOUDDQ_BIGQUERY_DATASET=clouddq_dataset
        export CLOUDDQ_TARGET_BIGQUERY_TABLE="<gcp-project-id>.clouddq_dataset.data_output"
* Get into the root folder of your CloudDQ deployment

## CloudDQ Launch
### Count
    python3 clouddq_executable.zip \
        DQ_COUNT \
        oss-dq \
        --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
        --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
        --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
        --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Nullability Controls
#### Missing values in columns
    python3 clouddq_executable.zip \
       DQ_NODE_ACCOUNT_VALUE_NOT_NULL,DQ_KPI_VALUE_VALUE_NOT_NULL \
        oss-dq \
        --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
        --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
        --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
        --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Duplicates
    python3 clouddq_executable.zip \
        DQ_KPI_DUPLICATE \
        oss-dq \
        --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
        --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
        --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
        --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"

### Presence of Keys
#### Foreign Key Enforcement
    python3 clouddq_executable.zip \
        DQ_FOREIGN_KEY_VALID \
        oss-dq \
        --gcp_project_id="${GOOGLE_CLOUD_PROJECT}" \
        --gcp_bq_dataset_id="${CLOUDDQ_BIGQUERY_DATASET}" \
        --gcp_region_id="${CLOUDDQ_BIGQUERY_REGION}" \
        --target_bigquery_summary_table="${CLOUDDQ_TARGET_BIGQUERY_TABLE}"
