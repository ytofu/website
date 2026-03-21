# Connect Instance Storage Config

Manage Connect Instance Storage Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_instance_storage_config:
    example:
      instance_id: ${aws_connect_instance.example.id}
      resource_type: CONTACT_TRACE_RECORDS
      storage_config:
        kinesis_firehose_config:
          firehose_arn: ${aws_kinesis_firehose_delivery_stream.example.arn}
        storage_type: KINESIS_FIREHOSE
```

## Storage Config Kinesis Stream Config

```yaml
resource:
  aws_connect_instance_storage_config:
    example:
      instance_id: ${aws_connect_instance.example.id}
      resource_type: CONTACT_TRACE_RECORDS
      storage_config:
        kinesis_stream_config:
          stream_arn: ${aws_kinesis_stream.example.arn}
        storage_type: KINESIS_STREAM
```

## Storage Config Kinesis Video Stream Config

```yaml
resource:
  aws_connect_instance_storage_config:
    example:
      instance_id: ${aws_connect_instance.example.id}
      resource_type: MEDIA_STREAMS
      storage_config:
        kinesis_video_stream_config:
          prefix: example
          retention_period_hours: 3
          encryption_config:
            encryption_type: KMS
            key_id: ${aws_kms_key.example.arn}
        storage_type: KINESIS_VIDEO_STREAM
```

## Storage Config S3 Config

```yaml
resource:
  aws_connect_instance_storage_config:
    example:
      instance_id: ${aws_connect_instance.example.id}
      resource_type: CHAT_TRANSCRIPTS
      storage_config:
        s3_config:
          bucket_name: ${aws_s3_bucket.example.id}
          bucket_prefix: example
        storage_type: S3
```

## Storage Config S3 Config with Encryption Config

```yaml
resource:
  aws_connect_instance_storage_config:
    example:
      instance_id: ${aws_connect_instance.example.id}
      resource_type: CHAT_TRANSCRIPTS
      storage_config:
        s3_config:
          bucket_name: ${aws_s3_bucket.example.id}
          bucket_prefix: example
          encryption_config:
            encryption_type: KMS
            key_id: ${aws_kms_key.example.arn}
        storage_type: S3
```
