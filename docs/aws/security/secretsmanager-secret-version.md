# Secretsmanager Secret Version

Manage Secretsmanager Secret Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-string-to-protect
```

## Key-Value Pairs

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-value
```
