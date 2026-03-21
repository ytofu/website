# Timestreamquery Scheduled Query

Manage Timestreamquery Scheduled Query resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_timestreamquery_scheduled_query:
    example:
      execution_role_arn: ${aws_iam_role.example.arn}
      name: ${aws_timestreamwrite_table.example.table_name}
      query_string: |
        SELECT region, az, hostname, BIN(time, 15s) AS binned_timestamp,
        ROUND(AVG(cpu_utilization), 2) AS avg_cpu_utilization,
        ROUND(APPROX_PERCENTILE(cpu_utilization, 0.9), 2) AS p90_cpu_utilization,
        ROUND(APPROX_PERCENTILE(cpu_utilization, 0.95), 2) AS p95_cpu_utilization,
        ROUND(APPROX_PERCENTILE(cpu_utilization, 0.99), 2) AS p99_cpu_utilization
        FROM exampledatabase.exampletable
        WHERE measure_name = 'metrics' AND time > ago(2h)
        GROUP BY region, hostname, az, BIN(time, 15s)
        ORDER BY binned_timestamp ASC
        LIMIT 5
      error_report_configuration:
        s3_configuration:
          bucket_name: ${aws_s3_bucket.example.bucket}
      notification_configuration:
        sns_configuration:
          topic_arn: ${aws_sns_topic.example.arn}
      schedule_configuration:
        schedule_expression: rate(1 hour)
      target_configuration:
        timestream_configuration:
          database_name: ${aws_timestreamwrite_database.results.database_name}
          table_name: ${aws_timestreamwrite_table.results.table_name}
          time_column: binned_timestamp
          dimension_mapping:
            dimension_value_type: VARCHAR
            name: az
          dimension_mapping:
            dimension_value_type: VARCHAR
            name: region
          dimension_mapping:
            dimension_value_type: VARCHAR
            name: hostname
          multi_measure_mappings:
            target_multi_measure_name: multi-metrics
            multi_measure_attribute_mapping:
              measure_value_type: DOUBLE
              source_column: avg_cpu_utilization
            multi_measure_attribute_mapping:
              measure_value_type: DOUBLE
              source_column: p90_cpu_utilization
            multi_measure_attribute_mapping:
              measure_value_type: DOUBLE
              source_column: p95_cpu_utilization
            multi_measure_attribute_mapping:
              measure_value_type: DOUBLE
              source_column: p99_cpu_utilization
```

## Multi-step Example

```yaml
resource:
  aws_s3_bucket:
    test:
      bucket: example
      force_destroy: true

resource:
  aws_sns_topic:
    test:
      name: example

resource:
  aws_sqs_queue:
    test:
      name: example
      sqs_managed_sse_enabled: true

resource:
  aws_sns_topic_subscription:
    test:
      topic_arn: ${aws_sns_topic.test.arn}
      protocol: sqs
      endpoint: ${aws_sqs_queue.test.arn}

resource:
  aws_sqs_queue_policy:
    test:
      queue_url: ${aws_sqs_queue.test.id}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Principal": { "AWS": "*" } "Action": ["sqs:SendMessage"] "Resource": aws_sqs_queue.test.arn "Condition": { "ArnEquals": { "aws:SourceArn" = aws_sns_topic.test.arn } } }] }'

resource:
  aws_iam_role:
    test:
      name: example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Principal": { "Service": "timestream.amazonaws.com" } "Action": "sts:AssumeRole" }] }'
      tags:
        Name: example

resource:
  aws_iam_role_policy:
    test:
      name: example
      role: ${aws_iam_role.test.id}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Action": [ "kms:Decrypt", "sns:Publish", "timestream:describeEndpoints", "timestream:Select", "timestream:SelectValues", "timestream:WriteRecords", "s3:PutObject", ] "Resource": "*" "Effect": "Allow" }] }'

resource:
  aws_timestreamwrite_database:
    test:
      database_name: exampledatabase

resource:
  aws_timestreamwrite_table:
    test:
      database_name: ${aws_timestreamwrite_database.test.database_name}
      table_name: exampletable
      magnetic_store_write_properties:
        enable_magnetic_store_writes: true
      retention_properties:
        magnetic_store_retention_period_in_days: 1
        memory_store_retention_period_in_hours: 1

resource:
  aws_timestreamwrite_database:
    results:
      database_name: exampledatabase-results

resource:
  aws_timestreamwrite_table:
    results:
      database_name: ${aws_timestreamwrite_database.results.database_name}
      table_name: exampletable-results
      magnetic_store_write_properties:
        enable_magnetic_store_writes: true
      retention_properties:
        magnetic_store_retention_period_in_days: 1
        memory_store_retention_period_in_hours: 1
```
