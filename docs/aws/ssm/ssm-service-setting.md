# Resource: aws_ssm_service_setting

This setting defines how a user interacts with or uses a service or a feature of a service.

## Basic Example

```yaml
resource:
  aws_ssm_service_setting:
    test_setting:
      setting_id: "arn:aws:ssm:us-east-1:123456789012:servicesetting/ssm/parameter-store/high-throughput-enabled"
      setting_value: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `setting_id` - (Required) ID of the service setting. Valid values are shown in the [AWS documentation](https://docs.aws.amazon.com/systems-manager/latest/APIReference/API_GetServiceSetting.html#API_GetServiceSetting_RequestSyntax).
* `setting_value` - (Required) Value of the service setting.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the service setting.
* `status` - Status of the service setting. Value can be `Default`, `Customized` or `PendingUpdate`.

## Import

```bash
ytofu import aws_ssm_service_setting.example arn:aws:ssm:us-east-1:123456789012:servicesetting/ssm/parameter-store/high-throughput-enabled
```
