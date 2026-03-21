# Gamelift Script

Manage Gamelift Script resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_gamelift_script:
    example:
      name: example-script
      storage_location:
        bucket: ${aws_s3_bucket.example.id}
        key: ${aws_s3_object.example.key}
        role_arn: ${aws_iam_role.example.arn}
```
