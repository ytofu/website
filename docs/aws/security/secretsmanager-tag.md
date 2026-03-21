# Secretsmanager Tag

Manage Secretsmanager Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret:
    test:
      name: example-secret
      lifecycle:
        ignore_changes: 
          - tags

resource:
  aws_secretsmanager_tag:
    test:
      secret_id: ${aws_secretsmanager_secret.test.id}
      key: ExampleKey
      value: ExampleValue
```
