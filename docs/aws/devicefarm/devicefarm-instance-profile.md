# Resource: aws_devicefarm_instance_profile

Provides a resource to manage AWS Device Farm Instance Profiles.
∂

## Basic Example

```yaml
resource:
  aws_devicefarm_instance_profile:
    example:
      name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The description of the instance profile.
* `exclude_app_packages_from_cleanup` - (Optional) An array of strings that specifies the list of app packages that should not be cleaned up from the device after a test run.
* `name` - (Required) The name for the instance profile.
* `package_cleanup` - (Optional) When set to `true`, Device Farm removes app packages after a test run. The default value is `false` for private devices.
* `reboot_after_use` - (Optional) When set to `true`, Device Farm reboots the instance after a test run. The default value is `true`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name of this instance profile.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_devicefarm_instance_profile.example arn:aws:devicefarm:us-west-2:123456789012:instanceprofile:4fa784c7-ccb4-4dbf-ba4f-02198320daa1
```
