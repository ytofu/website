# Secrets Manager Secret Version

Store secret values using ytofu YAML.

## String Secret

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example

  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: my-secret-value
```

## JSON Secret

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-json-policy
```

## Key/Value Secret

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-value
```
