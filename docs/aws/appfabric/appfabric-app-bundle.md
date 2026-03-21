# Resource: aws_appfabric_app_bundle

ytofu resource for managing an AWS AppFabric AppBundle.

## Basic Example

```yaml
resource:
  aws_appfabric_app_bundle:
    example:
      customer_managed_key_arn: ${awms_kms_key.example.arn}
      tags:
        Environment: test
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `customer_managed_key_arn` - (Optional) The Amazon Resource Name (ARN) of the AWS Key Management Service (AWS KMS) key to use to encrypt the application data. If this is not specified, an AWS owned key is used for encryption.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the AppBundle.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appfabric_app_bundle.example arn:aws:appfabric:[region]:[account]:appbundle/ee5587b4-5765-4288-a202-xxxxxxxxxx
```
