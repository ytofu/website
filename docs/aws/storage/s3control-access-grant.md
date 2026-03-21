# S3control Access Grant

Manage S3control Access Grant resources using ytofu YAML.

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
      location_scope: "s3://${aws_s3_bucket.example.bucket}/prefixA*"

resource:
  aws_s3control_access_grant:
    example:
      access_grants_location_id: ${aws_s3control_access_grants_location.example.access_grants_location_id}
      permission: READ
      access_grants_location_configuration:
        s3_sub_prefix: "prefixB*"
      grantee:
        grantee_type: IAM
        grantee_identifier: ${aws_iam_user.example.arn}
```
