# Glue Catalog Table

Manage Glue Catalog Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_catalog_table:
    example:
      name: MyCatalogTable
      database_name: MyCatalogDatabase
```

## Parquet Table for Athena

```yaml
resource:
  aws_glue_catalog_table:
    example:
      name: MyCatalogTable
      database_name: MyCatalogDatabase
      table_type: EXTERNAL_TABLE
      parameters:
        EXTERNAL: TRUE
      storage_descriptor:
        location: "s3://my-bucket/event-streams/my-stream"
        input_format: org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat
        output_format: org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat
        ser_de_info:
          name: my-stream
          serialization_library: org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe
          parameters: 
        columns:
          name: my_string
          type: string
        columns:
          name: my_double
          type: double
        columns:
          name: my_date
          type: date
          comment: 
        columns:
          name: my_bigint
          type: bigint
          comment: 
        columns:
          name: my_struct
          type: "struct<my_nested_string:string>"
          comment: 
```

## Iceberg Table

```yaml
resource:
  aws_glue_catalog_table:
    example:
      name: transactiontable1
      database_name: bankdata_icebergdb
      open_table_format_input:
        iceberg_input:
          metadata_operation: CREATE
          version: 2
          iceberg_table_input:
            location: "s3://sampledatabucket/bankdataiceberg/transactiontable1/"
            schema:
              schema_id: 0
              type: struct
              fields:
                id: 1
                name: transaction_id
                required: true
                type: |
                  "string"
              fields:
                id: 2
                name: transaction_date
                required: true
                type: |
                  "date"
              fields:
                id: 3
                name: monthly_balance
                required: true
                type: |
                  "float"
            partition_spec:
              fields:
                name: by_year
                source_id: 2
                transform: year
              spec_id: 0
            sort_order:
              fields:
                direction: asc
                null_order: nulls-last
                source_id: 1
                transform: none
              order_id: 1
```
