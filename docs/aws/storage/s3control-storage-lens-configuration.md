# S3control Storage Lens Configuration

Manage S3control Storage Lens Configuration resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_s3control_storage_lens_configuration:
    example:
      config_id: example-1
      storage_lens_configuration:
        enabled: true
        account_level:
          activity_metrics:
            enabled: true
          bucket_level:
            activity_metrics:
              enabled: true
        data_export:
          cloud_watch_metrics:
            enabled: true
          s3_bucket_destination:
            account_id: ${data.aws_caller_identity.current.account_id}
            arn: ${aws_s3_bucket.target.arn}
            format: CSV
            output_schema_version: V_1
            encryption:
              sse_s3:
          exclude:
            buckets: 
              - ${aws_s3_bucket.b1.arn}
              - ${aws_s3_bucket.b2.arn}
            regions: 
              - us-east-2
```
