# Networkfirewall Logging Configuration

Manage Networkfirewall Logging Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_logging_configuration:
    example:
      firewall_arn: ${aws_networkfirewall_firewall.example.arn}
      logging_configuration:
        log_destination_config:
          log_destination:
            bucketName: ${aws_s3_bucket.example.bucket}
            prefix: example
          log_destination_type: S3
          log_type: FLOW
```

## Logging to CloudWatch

```yaml
resource:
  aws_networkfirewall_logging_configuration:
    example:
      firewall_arn: ${aws_networkfirewall_firewall.example.arn}
      logging_configuration:
        log_destination_config:
          log_destination:
            logGroup: ${aws_cloudwatch_log_group.example.name}
          log_destination_type: CloudWatchLogs
          log_type: ALERT
```

## Logging to Kinesis Data Firehose

```yaml
resource:
  aws_networkfirewall_logging_configuration:
    example:
      firewall_arn: ${aws_networkfirewall_firewall.example.arn}
      logging_configuration:
        log_destination_config:
          log_destination:
            deliveryStream: ${aws_kinesis_firehose_delivery_stream.example.name}
          log_destination_type: KinesisDataFirehose
          log_type: TLS
```
