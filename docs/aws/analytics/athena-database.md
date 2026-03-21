# Athena Database

Manage Athena Database resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_athena_database:
    example:
      name: database_name
      bucket: ${aws_s3_bucket.example.id}
```
