# Resource: aws_config_retention_configuration

Provides a resource to manage the AWS Config retention configuration.
The retention configuration defines the number of days that AWS Config stores historical information.

## Basic Example

```yaml
resource:
  aws_config_retention_configuration:
    example:
      retention_period_in_days: 90
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `retention_period_in_days` - (Required) The number of days AWS Config stores historical information.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `name` - The name of the retention configuration object. The object is always named **default**.

## Import

```bash
ytofu import aws_config_retention_configuration.example default
```
