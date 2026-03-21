# Redshift Logging

Manage Redshift Logging resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_logging:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      log_destination_type: cloudwatch
      log_exports: 
        - connectionlog
        - userlog
```

## S3 Destination Type

```yaml
resource:
  aws_redshift_logging:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      log_destination_type: s3
      bucket_name: ${aws_s3_bucket.example.id}
      s3_key_prefix: example-prefix/
```
