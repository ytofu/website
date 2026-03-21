# Resource: aws_securityhub_standards_control_association

ytofu resource for managing an AWS Security Hub Standards Control Association.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_standards_subscription:
    cis_aws_foundations_benchmark:
      standards_arn: "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"
      depends_on: 
        - ${aws_securityhub_account.example}

resource:
  aws_securityhub_standards_control_association:
    cis_aws_foundations_benchmark_disable_iam_1:
      standards_arn: ${aws_securityhub_standards_subscription.cis_aws_foundations_benchmark.standards_arn}
      security_control_id: IAM.1
      association_status: DISABLED
      updated_reason: Not needed
```

## Argument Reference

The following arguments are required:

* `association_status` - (Required) The desired enablement status of the control in the standard. Valid values: `ENABLED`, `DISABLED`.
* `security_control_id` - (Required) The unique identifier for the security control whose enablement status you want to update.
* `standards_arn` - (Required) The Amazon Resource Name (ARN) of the standard in which you want to update the control's enablement status.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `updated_reason` - (Optional) The reason for updating the control's enablement status in the standard. Required when `association_status` is `DISABLED`.

## Attribute Reference

This resource exports no additional attributes.
