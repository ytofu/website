# Glue Data Catalog Encryption Settings

Manage Glue Data Catalog Encryption Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_data_catalog_encryption_settings:
    example:
      data_catalog_encryption_settings:
        connection_password_encryption:
          aws_kms_key_id: ${aws_kms_key.test.arn}
          return_connection_password_encrypted: true
        encryption_at_rest:
          catalog_encryption_mode: SSE-KMS
          catalog_encryption_service_role: ${aws_iam.role.test.arn}
          sse_aws_kms_key_id: ${aws_kms_key.test.arn}
```
