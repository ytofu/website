# Secrets Manager Secret Rotation

Configure automatic rotation for secrets using ytofu YAML.

## Basic Rotation

```yaml
resource:
  aws_secretsmanager_secret_rotation:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      rotation_lambda_arn: ${aws_lambda_function.example.arn}
      rotation_rules:
        automatically_after_days: 30
```

## With Schedule Expression

```yaml
resource:
  aws_secretsmanager_secret_rotation:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      rotation_lambda_arn: ${aws_lambda_function.example.arn}
      rotation_rules:
        schedule_expression: rate(7 days)
```
