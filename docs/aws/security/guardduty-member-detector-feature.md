# Resource: aws_guardduty_member_detector_feature

Provides a resource to manage a single Amazon GuardDuty [detector feature](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty-features-activation-model.html#guardduty-features) for a member account.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true

resource:
  aws_guardduty_member_detector_feature:
    runtime_monitoring:
      detector_id: ${aws_guardduty_detector.example.id}
      account_id: 123456789012
      name: S3_DATA_EVENTS
      status: ENABLED
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `detector_id` - (Required) Amazon GuardDuty detector ID.
* `account_id` - (Required) Member account ID to be updated.
* `name` - (Required) The name of the detector feature. Valid values: `S3_DATA_EVENTS`, `EKS_AUDIT_LOGS`, `EBS_MALWARE_PROTECTION`, `RDS_LOGIN_EVENTS`, `EKS_RUNTIME_MONITORING`,`RUNTIME_MONITORING`, `LAMBDA_NETWORK_LOGS`.
* `status` - (Required) The status of the detector feature. Valid values: `ENABLED`, `DISABLED`.
* `additional_configuration` - (Optional) Additional feature configuration block. See [below](#additional-configuration).

### Additional Configuration

The `additional_configuration` block supports the following:

* `name` - (Required) The name of the additional configuration. Valid values: `EKS_ADDON_MANAGEMENT`, `ECS_FARGATE_AGENT_MANAGEMENT`.
* `status` - (Required) The status of the additional configuration. Valid values: `ENABLED`, `DISABLED`.

## Attribute Reference

This resource exports no additional attributes.
