# Timestreamwrite Database

Manage Timestreamwrite Database resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_timestreamwrite_database:
    example:
      database_name: database-example
```

## Full usage

```yaml
resource:
  aws_timestreamwrite_database:
    example:
      database_name: database-example
      kms_key_id: ${aws_kms_key.example.arn}
      tags:
        Name: value
```
