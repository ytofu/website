# Resource: aws_computeoptimizer_enrollment_status

Manages AWS Compute Optimizer enrollment status.

## Basic Example

```yaml
resource:
  aws_computeoptimizer_enrollment_status:
    example:
      status: Active
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `include_member_accounts` - (Optional) Whether to enroll member accounts of the organization if the account is the management account of an organization. Default is `false`.
* `status` - (Required) The enrollment status of the account. Valid values: `Active`, `Inactive`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `number_of_member_accounts_opted_in` - The count of organization member accounts that are opted in to the service, if your account is an organization management account.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)

## Import

```bash
ytofu import aws_computeoptimizer_enrollment_status.example 123456789012
```
