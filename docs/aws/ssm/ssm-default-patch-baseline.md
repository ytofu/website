# Resource: aws_ssm_default_patch_baseline

ytofu resource for registering an AWS Systems Manager Default Patch Baseline.

## Basic Example

```yaml
resource:
  aws_ssm_default_patch_baseline:
    example:
      baseline_id: ${aws_ssm_patch_baseline.example.id}
      operating_system: ${aws_ssm_patch_baseline.example.operating_system}

resource:
  aws_ssm_patch_baseline:
    example:
      name: example
      approved_patches: 
        - KB123456
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `baseline_id` - (Required) ID of the patch baseline.
  Can be an ID or an ARN.
  When specifying an AWS-provided patch baseline, must be the ARN.
* `operating_system` - (Required) The operating system the patch baseline applies to.
  Valid values are
  `AMAZON_LINUX`,
  `AMAZON_LINUX_2`,
  `AMAZON_LINUX_2022`,
  `AMAZON_LINUX_2023`,
  `CENTOS`,
  `DEBIAN`,
  `MACOS`,
  `ORACLE_LINUX`,
  `RASPBIAN`,
  `REDHAT_ENTERPRISE_LINUX`,
  `ROCKY_LINUX`,
  `SUSE`,
  `UBUNTU`, and
  `WINDOWS`.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ssm_default_patch_baseline.example pb-1234567890abcdef1
```
