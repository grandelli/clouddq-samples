# DQ Tasks
This section contains the DQ Tasks for [Dataplex](https://cloud.google.com/dataplex/docs/data-quality-overview). These are the same examples included in the OSS CloudDQ section.

Before starting, have a look at the corresponding [Dataplex](https://cloud.google.com/dataplex/docs/check-data-quality#before_you_begin) documentation.

## DQ Tasks *vs* OSS CloudDQ
The main differences are:
* There's no need to create any entity config file in DQ Tasks. Tables can be directly referenced using the *[entity_uri](https://cloud.google.com/dataplex/docs/check-data-quality#example_specification_files)* attribute in the *rule_binding* section of the YAML files. In particular, it is possible to reference a table using the BQ syntax (e.g. *bigquery://projects/<project-id>/datasets/<dataset-id>/tables/<table-id>*) or the Dataplex syntax.
* You can provide a single YAML file embedding all the mandatory section, or you can keep each section as a separate YAML file, zip all of them, and provide the archive file to Dataplex. In this repo you will find both the approaches (see the corresponding subfolder).      

## Setup
Since DQ Tasks are managed by Dataplex, there's no need to install any CloudDQ executable. Nonetheless, the GCP project must be configured to successfully run DQ Tasks.

## DQ Tasks Launch
