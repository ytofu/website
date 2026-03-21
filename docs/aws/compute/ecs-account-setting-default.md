# Resource: aws_ecs_account_setting_default

Provides an ECS default account setting for a specific ECS Resource name within a specific region. More information can be found on the [ECS Developer Guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-account-settings.html).

## Basic Example

```yaml
resource:
  aws_ecs_account_setting_default:
    test:
      name: taskLongArnFormat
      value: enabled
```

## Set the default log driver mode to non-blocking

```yaml
resource:
  aws_ecs_account_setting_default:
    test:
      name: defaultLogDriverMode
      value: non-blocking
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the account setting to set.
* `value` - (Required) State of the setting.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `prinicpal_arn` - ARN that identifies the account setting.

## Import

```bash
ytofu import aws_ecs_account_setting_default.example taskLongArnFormat
```
