# Resource: aws_account_region

Enable (Opt-In) or Disable (Opt-Out) a particular Region for an AWS account.

## Basic Example

```yaml
resource:
  aws_account_region:
    example:
      region_name: ap-southeast-3
      enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `account_id` - (Optional) The ID of the target account when managing member accounts. Will manage current user's account by default if omitted. To use this parameter, the caller must be an identity in the organization's management account or a delegated administrator account. The specified account ID must also be a member account in the same organization. The organization must have all features enabled, and the organization must have trusted access enabled for the Account Management service, and optionally a delegated admin account assigned.
* `enabled` - (Required) Whether the region is enabled.
* `region_name` - (Required) The region name to manage.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `opt_status` - The region opt status.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `60m`)

## Import

```bash
ytofu import aws_account_region.example ap-southeast-3
```
