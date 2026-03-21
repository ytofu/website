# Resource: aws_s3control_object_lambda_access_point_policy

Provides a resource to manage an S3 Object Lambda Access Point resource policy.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_access_point:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: example

resource:
  aws_s3control_object_lambda_access_point:
    example:
      name: example
      configuration:
        supporting_access_point: ${aws_s3_access_point.example.arn}
        transformation_configuration:
          actions: 
            - GetObject
          content_transformation:
            aws_lambda:
              function_arn: ${aws_lambda_function.example.arn}

resource:
  aws_s3control_object_lambda_access_point_policy:
    example:
      name: ${aws_s3control_object_lambda_access_point.example.name}
      policy: '{ "Version": "2008-10-17" "Statement": [{ "Effect": "Allow" "Action": "s3-object-lambda:GetObject" "Principal": { "AWS": data.aws_caller_identity.current.account_id } "Resource": aws_s3control_object_lambda_access_point.example.arn }] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Optional) The AWS account ID for the account that owns the Object Lambda Access Point. Defaults to automatically determined account ID of the ytofu AWS provider.
* `name` - (Required) The name of the Object Lambda Access Point.
* `policy` - (Required) The Object Lambda Access Point resource policy document.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `has_public_access_policy` - Indicates whether this access point currently has a policy that allows public access.
* `id` - The AWS account ID and access point name separated by a colon (`:`).

## Import

```bash
ytofu import aws_s3control_object_lambda_access_point_policy.example 123456789012:example
```
