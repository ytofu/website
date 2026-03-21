# Appfabric Ingestion Destination

Manage Appfabric Ingestion Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appfabric_ingestion_destination:
    example:
      app_bundle_arn: ${aws_appfabric_app_bundle.example.arn}
      ingestion_arn: ${aws_appfabric_ingestion.example.arn}
      processing_configuration:
        audit_log:
          format: json
          schema: raw
      destination_configuration:
        audit_log:
          destination:
            s3_bucket:
              bucket_name: ${aws_s3_bucket.example.bucket}
```
