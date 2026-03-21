# Resource: aws_sesv2_account_vdm_attributes

ytofu resource for managing an AWS SESv2 (Simple Email V2) Account VDM Attributes.

## Basic Example

```yaml
resource:
  aws_sesv2_account_vdm_attributes:
    example:
      vdm_enabled: ENABLED
      dashboard_attributes:
        engagement_metrics: ENABLED
      guardian_attributes:
        optimized_shared_delivery: ENABLED
```

## Argument Reference

The following arguments are required:

* `vdm_enabled` - (Required) Specifies the status of your VDM configuration. Valid values: `ENABLED`, `DISABLED`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `dashboard_attributes` - (Optional) Specifies additional settings for your VDM configuration as applicable to the Dashboard.
* `guardian_attributes` - (Optional) Specifies additional settings for your VDM configuration as applicable to the Guardian.

### dashboard_attributes

* `engagement_metrics` - (Optional) Specifies the status of your VDM engagement metrics collection. Valid values: `ENABLED`, `DISABLED`.

### guardian_attributes

* `optimized_shared_delivery` - (Optional) Specifies the status of your VDM optimized shared delivery. Valid values: `ENABLED`, `DISABLED`.

## Attribute Reference

This data source exports no additional attributes.

## Import

```bash
ytofu import aws_sesv2_account_vdm_attributes.example ses-account-vdm-attributes
```
