# Kinesisanalyticsv2 Application

Manage Kinesisanalyticsv2 Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-flink-application

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example.id}
      key: example-flink-application
      source: flink-app.jar

resource:
  aws_kinesisanalyticsv2_application:
    example:
      name: example-flink-application
      runtime_environment: FLINK-1_8
      service_execution_role: ${aws_iam_role.example.arn}
      application_configuration:
        application_code_configuration:
          code_content:
            s3_content_location:
              bucket_arn: ${aws_s3_bucket.example.arn}
              file_key: ${aws_s3_object.example.key}
          code_content_type: ZIPFILE
        environment_properties:
          property_group:
            property_group_id: PROPERTY-GROUP-1
            property_map:
              Key1: Value1
          property_group:
            property_group_id: PROPERTY-GROUP-2
            property_map:
              KeyA: ValueA
              KeyB: ValueB
        flink_application_configuration:
          checkpoint_configuration:
            configuration_type: DEFAULT
          monitoring_configuration:
            configuration_type: CUSTOM
            log_level: DEBUG
            metrics_level: TASK
          parallelism_configuration:
            auto_scaling_enabled: true
            configuration_type: CUSTOM
            parallelism: 10
            parallelism_per_kpu: 4
      tags:
        Environment: test
```

## SQL Application

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example-sql-application

resource:
  aws_cloudwatch_log_stream:
    example:
      name: example-sql-application
      log_group_name: ${aws_cloudwatch_log_group.example.name}

resource:
  aws_kinesisanalyticsv2_application:
    example:
      name: example-sql-application
      runtime_environment: SQL-1_0
      service_execution_role: ${aws_iam_role.example.arn}
      application_configuration:
        application_code_configuration:
          code_content:
            text_content: SELECT 1;\n
          code_content_type: PLAINTEXT
        sql_application_configuration:
          input:
            name_prefix: PREFIX_1
            input_parallelism:
            input_schema:
              record_column:
                name: COLUMN_1
                sql_type: VARCHAR(8)
                mapping: MAPPING-1
              record_column:
                name: COLUMN_2
                sql_type: DOUBLE
              record_encoding: UTF-8
              record_format:
                record_format_type: CSV
                mapping_parameters:
                  csv_mapping_parameters:
                    record_column_delimiter: ","
                    record_row_delimiter: \n
            kinesis_streams_input:
              resource_arn: ${aws_kinesis_stream.example.arn}
          output:
            name: OUTPUT_1
            destination_schema:
              record_format_type: JSON
            lambda_output:
              resource_arn: ${aws_lambda_function.example.arn}
          output:
            name: OUTPUT_2
            destination_schema:
              record_format_type: CSV
            kinesis_firehose_output:
              resource_arn: ${aws_kinesis_firehose_delivery_stream.example.arn}
          reference_data_source:
            table_name: TABLE-1
            reference_schema:
              record_column:
                name: COLUMN_1
                sql_type: INTEGER
              record_format:
                record_format_type: JSON
                mapping_parameters:
                  json_mapping_parameters:
                    record_row_path: $
            s3_reference_data_source:
              bucket_arn: ${aws_s3_bucket.example.arn}
              file_key: KEY-1
      cloudwatch_logging_options:
        log_stream_arn: ${aws_cloudwatch_log_stream.example.arn}
```

## VPC Configuration

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-flink-application

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example.id}
      key: example-flink-application
      source: flink-app.jar

resource:
  aws_kinesisanalyticsv2_application:
    example:
      name: example-flink-application
      runtime_environment: FLINK-1_8
      service_execution_role: ${aws_iam_role.example.arn}
      application_configuration:
        application_code_configuration:
          code_content:
            s3_content_location:
              bucket_arn: ${aws_s3_bucket.example.arn}
              file_key: ${aws_s3_object.example.key}
          code_content_type: ZIPFILE
        vpc_configuration:
          security_group_ids: 
            - ${aws_security_group.example[0].id}
            - ${aws_security_group.example[1].id}
          subnet_ids: 
            - ${aws_subnet.example.id}
```
