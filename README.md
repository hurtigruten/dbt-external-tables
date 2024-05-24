# Fork of dbt-external-tables
This repo is a fork of [dbt-external-tables](https://github.com/dbt-labs/dbt-external-tables)
with a few minor changes to better work with Databricks.
It is not intended to be a full replacement for the original project. 

## Recover partitions
Spark & Databricks can automatically detect and recover partitions and infer full schema without
explicitly specifying the schema or partitions in the sources specification YAML files,
but this is not supported by dbt-external-tables version 0.9.0.
This fork allows automatic recovery of the partitions when `recover_partitions` flag is added:
````
- name: my_external_table
    external:
      using: parquet
      location: "<path to files>"
      recover_partitions: true
````

## Support for catalogs
Version 0.9.0 of dbt-external-tables does not work correctly with Databricks Catalogs. This causes `stage_external_sources` to always drop tables and do a full refresh, which is very slow. This is fixed here, but probably breaks compatibility with Spark.
