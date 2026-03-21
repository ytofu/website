# Verifiedaccess Instance Logging Configuration

Manage Verifiedaccess Instance Logging Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        cloudwatch_logs:
          enabled: true
          log_group: ${aws_cloudwatch_log_group.example.id}
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## With Kinesis Data Firehose Logging

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        kinesis_data_firehose:
          delivery_stream: ${aws_kinesis_firehose_delivery_stream.example.name}
          enabled: true
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## With S3 logging

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        s3:
          bucket_name: ${aws_s3_bucket.example.id}
          enabled: true
          prefix: example
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## With all three logging options

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        cloudwatch_logs:
          enabled: true
          log_group: ${aws_cloudwatch_log_group.example.id}
        kinesis_data_firehose:
          delivery_stream: ${aws_kinesis_firehose_delivery_stream.example.name}
          enabled: true
        s3:
          bucket_name: ${aws_s3_bucket.example.id}
          enabled: true
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## With `include_trust_context`

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        include_trust_context: true
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## With `log_version`

```yaml
resource:
  aws_verifiedaccess_instance_logging_configuration:
    example:
      access_logs:
        log_version: ocsf-1.0.0-rc.2
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```
