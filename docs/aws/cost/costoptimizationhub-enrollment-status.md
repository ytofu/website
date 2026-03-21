# Resource: aws_costoptimizationhub_enrollment_status

ytofu resource for managing AWS Cost Optimization Hub Enrollment Status.

## Basic Example

```yaml
resource:
  aws_costoptimizationhub_enrollment_status:
    example:
```

## Usage with all the arguments

```yaml
resource:
  aws_costoptimizationhub_enrollment_status:
    example:
      include_member_accounts: true
```

## Argument Reference

The following arguments are optional:

* `include_member_accounts` - (Optional) Flag to enroll member accounts of the organization if the account is the management account. No drift detection is currently supported for this argument. Default value is `false`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `status` - Status of enrollment. When the resource is present in ytofu, its status will always be `Active`.

## Import

```bash
ytofu import aws_costoptimizationhub_enrollment_status.example 111222333444
```
