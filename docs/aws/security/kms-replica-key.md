# KMS Replica Key

Manage KMS Replica Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    primary:
      description: Multi-Region primary key
      deletion_window_in_days: 30
      multi_region: true

resource:
  aws_kms_replica_key:
    replica:
      description: Multi-Region replica key
      deletion_window_in_days: 7
      primary_key_arn: ${aws_kms_key.primary.arn}
```

## Terraform AWS Provider v6 (and above)

```yaml
resource:
  aws_kms_key:
    primary:
      region: us-east-1
      description: Multi-Region primary key
      deletion_window_in_days: 30
      multi_region: true

resource:
  aws_kms_replica_key:
    replica:
      description: Multi-Region replica key
      deletion_window_in_days: 7
      primary_key_arn: ${aws_kms_key.primary.arn}
```
