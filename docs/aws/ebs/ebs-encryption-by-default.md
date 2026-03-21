# Resource: aws_ebs_encryption_by_default

Provides a resource to manage whether default EBS encryption is enabled for your AWS account in the current AWS region. To manage the default KMS key for the region, see the `aws_ebs_default_kms_key` resource.

## Basic Example

```yaml
resource:
  aws_ebs_encryption_by_default:
    example:
      enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `enabled` - (Optional) Whether or not default EBS encryption is enabled. Valid values are `true` or `false`. Defaults to `true`.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ebs_encryption_by_default.example default
```
