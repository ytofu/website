# SFN Activity

Manage SFN Activity resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sfn_activity:
    sfn_activity:
      name: my-activity
```

## Encryption

```yaml
resource:
  aws_sfn_activity:
    sfn_activity:
      name: my-activity
      encryption_configuration:
        kms_key_id: ${aws_kms_key.kms_key_for_sfn.arn}
        type: CUSTOMER_MANAGED_KMS_KEY
        kms_data_key_reuse_period_seconds: 900
```
