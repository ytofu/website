# Resource: aws_xray_encryption_config

Creates and manages an AWS XRay Encryption Config.

## Basic Example

```yaml
resource:
  aws_xray_encryption_config:
    example:
      type: NONE
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `type` - (Required) The type of encryption. Set to `KMS` to use your own key for encryption. Set to `NONE` for default encryption.
* `key_id` - (Optional) An AWS KMS customer master key (CMK) ARN.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Region name.

## Import

```bash
ytofu import aws_xray_encryption_config.example us-west-2
```
