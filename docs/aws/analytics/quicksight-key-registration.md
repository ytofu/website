# Resource: aws_quicksight_key_registration

Registers customer managed keys in a Amazon QuickSight account.

## Basic Example

```yaml
resource:
  aws_quicksight_key_registration:
    example:
      key_registration:
        key_arn: ${aws_kms_key.example1.arn}
      key_registration:
        key_arn: ${aws_kms_key.example2.arn}
        default_key: true
```

## Argument Reference

This resource supports the following arguments:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `key_registration` - (Required) Registered keys. See [key_registration](#key_registration).
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### key_registration

* `default_key` - (Optional) Whether the key is set as the default key for encryption and decryption use.
* `key_arn` - (Required) ARN of the AWS KMS key that is registered for encryption and decryption use.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_quicksight_key_registration.example "012345678901"
```
