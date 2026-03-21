# S3control Access Grants Instance Resource Policy

Manage S3control Access Grants Instance Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3control_access_grants_instance:
    example:

resource:
  aws_s3control_access_grants_instance_resource_policy:
    example:
      policy: |
        {
        "Version": "2012-10-17",
        "Id": "S3AccessGrantsPolicy",
        "Statement": [{
        "Sid": "AllowAccessToS3AccessGrants",
        "Effect": "Allow",
        "Principal": {
        "AWS": "123456789456"
        },
        "Action": [
        "s3:ListAccessGrants",
        "s3:ListAccessGrantsLocations",
        "s3:GetDataAccess"
        ],
        "Resource": "${aws_s3control_access_grants_instance.example.access_grants_instance_arn}"
        }]
        }
```
