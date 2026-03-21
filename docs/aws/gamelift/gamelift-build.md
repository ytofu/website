# Gamelift Build

Manage Gamelift Build resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_gamelift_build:
    test:
      name: example-build
      operating_system: WINDOWS_2012
      storage_location:
        bucket: ${aws_s3_bucket.test.id}
        key: ${aws_s3_object.test.key}
        role_arn: ${aws_iam_role.test.arn}
```
