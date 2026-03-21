# Resource: aws_vpc_ipam_organization_admin_account

Enables the IPAM Service and promotes a delegated administrator.

## Basic Example

```yaml
resource:
  aws_vpc_ipam_organization_admin_account:
    example:
      delegated_admin_account_id: ${data.aws_caller_identity.delegated.account_id}

data:
  aws_caller_identity:
    delegated:
```

## Argument Reference

This resource supports the following arguments:

* `delegated_admin_account_id` - (Required)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Organizations ARN for the delegate account.
* `id` - The Organizations member account ID that you want to enable as the IPAM account.
* `email` - The Organizations email for the delegate account.
* `name` - The Organizations name for the delegate account.
* `service_principal` - The AWS service principal.

## Import

```bash
ytofu import aws_vpc_ipam_organization_admin_account.example 12345678901
```
