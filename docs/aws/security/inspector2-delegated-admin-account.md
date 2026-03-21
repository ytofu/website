# Resource: aws_inspector2_delegated_admin_account

ytofu resource for managing an Amazon Inspector Delegated Admin Account.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_inspector2_delegated_admin_account:
    example:
      account_id: ${data.aws_caller_identity.current.account_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Required) Account to enable as delegated admin account.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `relationship_status` - Status of this delegated admin account.

## Timeouts

Configuration options:

* `create` - (Default `15m`)
* `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_inspector2_delegated_admin_account.example 123456789012
```
