# Resource: aws_licensemanager_license_configuration

Provides a License Manager license configuration resource.

## Basic Example

```yaml
resource:
  aws_licensemanager_license_configuration:
    example:
      name: Example
      description: Example
      license_count: 10
      license_count_hard_limit: true
      license_counting_type: Socket
      license_rules:
        - "#minimumSockets=2"
      tags:
        foo: barr
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the license configuration.
* `description` - (Optional) Description of the license configuration.
* `license_count` - (Optional) Number of licenses managed by the license configuration.
* `license_count_hard_limit` - (Optional) Sets the number of available licenses as a hard limit.
* `license_counting_type` - (Required) Dimension to use to track license inventory. Specify either `vCPU`, `Instance`, `Core` or `Socket`.
* `license_rules` - (Optional) Array of configured License Manager rules.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The license configuration ARN.
* `id` - The license configuration ARN.
* `owner_account_id` - Account ID of the owner of the license configuration.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_licensemanager_license_configuration.example arn:aws:license-manager:eu-west-1:123456789012:license-configuration:lic-0123456789abcdef0123456789abcdef
```
