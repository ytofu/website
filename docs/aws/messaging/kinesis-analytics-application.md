# Kinesis Analytics Application

Manage Kinesis Analytics Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesis_stream:
    test_stream:
      name: terraform-kinesis-test
      shard_count: 1

resource:
  aws_kinesis_analytics_application:
    test_application:
      name: kinesis-analytics-application-test
      inputs:
        name_prefix: test_prefix
        kinesis_stream:
          resource_arn: ${aws_kinesis_stream.test_stream.arn}
          role_arn: ${aws_iam_role.test.arn}
        parallelism:
        schema:
          record_columns:
            mapping: $.test
            name: test
            sql_type: VARCHAR(8)
          record_encoding: UTF-8
          record_format:
            mapping_parameters:
              json:
                record_row_path: $
```

## Starting An Application

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: analytics

resource:
  aws_cloudwatch_log_stream:
    example:
      name: example-kinesis-application
      log_group_name: ${aws_cloudwatch_log_group.example.name}

resource:
  aws_kinesis_stream:
    example:
      name: example-kinesis-stream
      shard_count: 1

resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: example-kinesis-delivery-stream
      destination: extended_s3
      extended_s3_configuration:
        bucket_arn: ${aws_s3_bucket.example.arn}
        role_arn: ${aws_iam_role.example.arn}

resource:
  aws_kinesis_analytics_application:
    test:
      name: example-application
      cloudwatch_logging_options:
        log_stream_arn: ${aws_cloudwatch_log_stream.example.arn}
        role_arn: ${aws_iam_role.example.arn}
      inputs:
        name_prefix: example_prefix
        schema:
          record_columns:
            name: COLUMN_1
            sql_type: INTEGER
          record_format:
            mapping_parameters:
              csv:
                record_column_delimiter: ","
                record_row_delimiter: "|"
        kinesis_stream:
          resource_arn: ${aws_kinesis_stream.example.arn}
          role_arn: ${aws_iam_role.example.arn}
        starting_position_configuration:
          starting_position: NOW
      outputs:
        name: OUTPUT_1
        schema:
          record_format_type: CSV
        kinesis_firehose:
          resource_arn: ${aws_kinesis_firehose_delivery_stream.example.arn}
          role_arn: ${aws_iam_role.example.arn}
      start_application: true
```
