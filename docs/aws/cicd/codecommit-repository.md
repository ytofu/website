# Codecommit Repository

Manage Codecommit Repository resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codecommit_repository:
    test:
      repository_name: MyTestRepository
      description: This is the Sample App Repository
```

## AWS KMS Customer Managed Keys (CMK)

```yaml
resource:
  aws_codecommit_repository:
    test:
      repository_name: MyTestRepository
      description: This is the Sample App Repository
      kms_key_id: ${aws_kms_key.test.arn}

resource:
  aws_kms_key:
    test:
      description: test
      deletion_window_in_days: 7
```
