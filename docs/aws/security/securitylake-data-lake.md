# Securitylake Data Lake

Manage Securitylake Data Lake resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securitylake_data_lake:
    example:
      meta_store_manager_role_arn: ${aws_iam_role.meta_store_manager.arn}
      configuration:
        region: eu-west-1
        encryption_configuration:
          kms_key_id: S3_MANAGED_KEY
        lifecycle_configuration:
          transition:
            days: 31
            storage_class: STANDARD_IA
          transition:
            days: 80
            storage_class: ONEZONE_IA
          expiration:
            days: 300
```

## Basic Usage

```yaml
resource:
  aws_securitylake_data_lake:
    example:
      meta_store_manager_role_arn: ${aws_iam_role.meta_store_manager.arn}
      configuration:
        region: eu-west-1
        encryption_configuration:
          kms_key_id: S3_MANAGED_KEY
```
