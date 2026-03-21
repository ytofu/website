# Resource: aws_cloudtrail_organization_delegated_admin_account

Provides a resource to manage an AWS CloudTrail Delegated Administrator.

## Basic Example

```yaml
resource:
  aws_cloudtrail_organization_delegated_admin_account:
    example:
      account_id: ${data.aws_caller_identity.delegated.account_id}

data:
  aws_caller_identity:
    delegated:
```

## Argument Reference

This resource supports the following arguments:

* `account_id` - (Required) An organization member account ID that you want to designate as a delegated administrator.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the delegated administrator's account.
* `email` - The email address that is associated with the delegated administrator's AWS account.
* `name` - The friendly name of the delegated administrator's account.
* `service_principal` - The AWS CloudTrail service principal name.

## Import

```bash
ytofu import aws_cloudtrail_organization_delegated_admin_account.example 12345678901
```
