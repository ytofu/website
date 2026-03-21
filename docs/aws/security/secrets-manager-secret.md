# Secrets Manager Secret

Create and manage secrets using ytofu YAML.

## Basic Secret

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret
      description: My secret
      tags:
        Environment: production
```

## With KMS Key

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret
      kms_key_id: ${aws_kms_key.example.id}
```

## With Recovery Window

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret
      recovery_window_in_days: 7
```
