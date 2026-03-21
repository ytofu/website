# Quicksight Data Set

Manage Quicksight Data Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: Column1
            type: STRING
          upload_settings:
            format: JSON
```

## With use_as

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      use_as: RLS_RULES
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: UserName
            type: STRING
          upload_settings:
            format: JSON
```

## With Column Level Permission Rules

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: Column1
            type: STRING
          upload_settings:
            format: JSON
      column_level_permission_rules:
        column_names: 
          - Column1
        principals: 
          - ${aws_quicksight_user.example.arn}
```

## With Field Folders

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: Column1
            type: STRING
          upload_settings:
            format: JSON
      field_folders:
        field_folders_id: example-id
        columns: 
          - Column1
        description: example description
```

## With Permissions

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: Column1
            type: STRING
          upload_settings:
            format: JSON
      permissions:
        actions:
          - "quicksight:DescribeDataSet"
          - "quicksight:DescribeDataSetPermissions"
          - "quicksight:PassDataSet"
          - "quicksight:DescribeIngestion"
          - "quicksight:ListIngestions"
        principal: ${aws_quicksight_user.example.arn}
```

## With Row Level Permission Tag Configuration

```yaml
resource:
  aws_quicksight_data_set:
    example:
      data_set_id: example-id
      name: example-name
      import_mode: SPICE
      physical_table_map:
        physical_table_map_id: example-id
        s3_source:
          data_source_arn: ${aws_quicksight_data_source.example.arn}
          input_columns:
            name: Column1
            type: STRING
          upload_settings:
            format: JSON
      row_level_permission_tag_configuration:
        status: ENABLED
        tag_rules:
          column_name: Column1
          tag_key: tagkey
          match_all_value: "*"
          tag_multi_value_delimiter: ","
```
