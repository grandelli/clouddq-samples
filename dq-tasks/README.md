# DQ Tasks
This section contains the DQ Tasks for [Dataplex](https://cloud.google.com/dataplex/docs/data-quality-overview). These are the same examples included in the OSS CloudDQ section.

Before starting, have a look at the corresponding [Dataplex](https://cloud.google.com/dataplex/docs/check-data-quality#before_you_begin) documentation.

## DQ Tasks *vs* OSS CloudDQ
The main differences are:
* There's no need to create any entity config file in DQ Tasks. Tables can be directly referenced using the *[entity_uri](https://cloud.google.com/dataplex/docs/check-data-quality#example_specification_files)* attribute in the *rule_binding* section of the YAML files. In particular, it is possible to reference a table using the BQ syntax (e.g. *bigquery://projects/<project-id>/datasets/<dataset-id>/tables/<table-id>*) or the Dataplex syntax.
* You can provide a single YAML file embedding all the mandatory section, or you can keep each section as a separate YAML file, zip all of them, and provide the archive file to Dataplex. In this repo you will find both the approaches (see the corresponding subfolder).      

## Setup
Since DQ Tasks are managed by Dataplex, there's no need to install any CloudDQ executable. Nonetheless, the GCP project must be configured to successfully run DQ Tasks.
  
It's extremely important that you follow all the steps reported in the [Before you begin](https://cloud.google.com/dataplex/docs/check-data-quality#before_you_begin) section of the Dataplex's documentation.

## Run

## Troubleshooting
##### When launching the DQ Task I get the following error in the serverless Spark job: "External network access. Drivers and executors have internal IP addresses. You can set up Cloud NAT to allow outbound traffic using internal IPs on your VPC network".
Fix this by running the following command (you need to fill in your own params):
  
    gcloud compute firewall-rules create allow-internal-ingress \
    --network="network-name" \
    --source-ranges="subnetwork internal-IP ranges" \
    --direction="ingress" \
    --action="allow" \
    --rules="all"

Typically, the network name is *default*, while the source range depends on the subnet and the location you're using to run the job (e.g. in my case in EU it was 10.132.0.0/20).
