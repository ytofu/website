# Resource: aws_apprunner_default_auto_scaling_configuration_version

Manages the default App Runner auto scaling configuration.
When creating or updating this resource the existing default auto scaling configuration will be set to non-default automatically.
When creating or updating this resource the configuration is automatically assigned as the default to the new services you create in the future. The new default designation doesn't affect the associations that were previously set for existing services.
Each account can have only one default auto scaling configuration per Region.

## Basic Example

```yaml
resource:
  aws_apprunner_auto_scaling_configuration_version:
    example:
      auto_scaling_configuration_name: example
      max_concurrency: 50
      max_size: 10
      min_size: 2

  aws_apprunner_default_auto_scaling_configuration_version:
    example:
      auto_scaling_configuration_arn: ${aws_apprunner_auto_scaling_configuration_version.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `auto_scaling_configuration_arn` - (Required) The ARN of the App Runner auto scaling configuration that you want to set as the default.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_apprunner_default_auto_scaling_configuration_version.example us-west-2
```
