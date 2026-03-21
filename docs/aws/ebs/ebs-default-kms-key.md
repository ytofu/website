# Resource: aws_ebs_default_kms_key

Provides a resource to manage the default customer master key (CMK) that your AWS account uses to encrypt EBS volumes.

## Basic Example

```yaml
resource:
  aws_ebs_default_kms_key:
    example:
      key_arn: ${aws_kms_key.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `key_arn` - (Required, ForceNew) The ARN of the AWS Key Management Service (AWS KMS) customer master key (CMK) to use to encrypt the EBS volume.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ebs_default_kms_key.example arn:aws:kms:us-east-1:123456789012:key/abcd-1234
```
