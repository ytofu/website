# S3control Access Grants Location

Manage S3control Access Grants Location resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3control_access_grants_instance:
    example:

resource:
  aws_s3control_access_grants_location:
    example:
      depends_on: 
        - ${aws_s3control_access_grants_instance.example}
      iam_role_arn: ${aws_iam_role.example.arn}
      location_scope: "s3://" # Default scope.
```
