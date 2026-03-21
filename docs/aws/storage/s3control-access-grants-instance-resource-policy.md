# Resource: aws_s3control_access_grants_instance_resource_policy

Provides a resource to manage an S3 Access Grants instance resource policy.
Use a resource policy to manage cross-account access to your S3 Access Grants instance.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Optional) The AWS account ID for the S3 Access Grants instance. Defaults to automatically determined account ID of the ytofu AWS provider.
* `policy` - (Optional) The policy document.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3control_access_grants_instance_resource_policy.example 123456789012
```
