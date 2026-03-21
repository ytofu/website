# Glue Partition Index

Manage Glue Partition Index resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_catalog_database:
    example:
      name: example

resource:
  aws_glue_catalog_table:
    example:
      name: example
      database_name: ${aws_glue_catalog_database.example.name}
      owner: my_owner
      retention: 1
      table_type: VIRTUAL_VIEW
      view_expanded_text: view_expanded_text_1
      view_original_text: view_original_text_1
      storage_descriptor:
        bucket_columns: 
          - bucket_column_1
        compressed: false
        input_format: SequenceFileInputFormat
        location: my_location
        number_of_buckets: 1
        output_format: SequenceFileInputFormat
        stored_as_sub_directories: false
        parameters:
          param1: param1_val
        columns:
          name: my_column_1
          type: int
          comment: my_column1_comment
        columns:
          name: my_column_2
          type: string
          comment: my_column2_comment
        ser_de_info:
          name: ser_de_name
          parameters:
            param1: param_val_1
          serialization_library: org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe
        sort_columns:
          column: my_column_1
          sort_order: 1
        skewed_info:
          skewed_column_names:
            - my_column_1
          skewed_column_value_location_maps:
            my_column_1: my_column_1_val_loc_map
          skewed_column_values:
            - skewed_val_1
      partition_keys:
        name: my_column_1
        type: int
        comment: my_column_1_comment
      partition_keys:
        name: my_column_2
        type: string
        comment: my_column_2_comment
      parameters:
        param1: param1_val

resource:
  aws_glue_partition_index:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      table_name: ${aws_glue_catalog_table.example.name}
      partition_index:
        index_name: example
        keys: 
          - my_column_1
          - my_column_2
```
