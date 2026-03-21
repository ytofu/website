# Resource: aws_s3control_access_grants_instance

Provides a resource to manage an S3 Access Grants instance, which serves as a logical grouping for access grants.
You can have one S3 Access Grants instance per Region in your account.

## Basic Example

```yaml
resource:
  aws_s3control_access_grants_instance:
    example:
```

## AWS IAM Identity Center

```yaml
resource:
  aws_s3control_access_grants_instance:
    example:
      identity_center_arn: "arn:aws:sso:::instance/ssoins-890759e9c7bfdc1d"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Optional) The AWS account ID for the S3 Access Grants instance. Defaults to automatically determined account ID of the ytofu AWS provider.
* `identity_center_arn` - (Optional) The ARN of the AWS IAM Identity Center instance associated with the S3 Access Grants instance.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `access_grants_instance_arn` - Amazon Resource Name (ARN) of the S3 Access Grants instance.
* `access_grants_instance_id` - Unique ID of the S3 Access Grants instance.
* `identity_center_application_arn` - The ARN of the AWS IAM Identity Center instance application; a subresource of the original Identity Center instance.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_s3control_access_grants_instance.example 123456789012
```
