# Resource: aws_securityhub_account

Enables Security Hub for this AWS account.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `enable_default_standards` - (Optional) Whether to enable the security standards that Security Hub has designated as automatically enabled including: ` AWS Foundational Security Best Practices v1.0.0` and `CIS AWS Foundations Benchmark v1.2.0`. Defaults to `true`.
* `control_finding_generator` - (Optional) Updates whether the calling account has consolidated control findings turned on. If the value for this field is set to `SECURITY_CONTROL`, Security Hub generates a single finding for a control check even when the check applies to multiple enabled standards. If the value for this field is set to `STANDARD_CONTROL`, Security Hub generates separate findings for a control check when the check applies to multiple enabled standards. For accounts that are part of an organization, this value can only be updated in the administrator account.
* `auto_enable_controls` - (Optional) Whether to automatically enable new controls when they are added to standards that are enabled. By default, this is set to true, and new controls are enabled automatically. To not automatically enable new controls, set this to false.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Account ID.
* `arn` - ARN of the SecurityHub Hub created in the account.

## Import

```bash
ytofu import aws_securityhub_account.example 123456789012
```
