# Resource: aws_macie2_organization_admin_account

Provides a resource to manage an [Amazon Macie Organization Admin Account](https://docs.aws.amazon.com/macie/latest/APIReference/admin.html).

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

  aws_macie2_organization_admin_account:
    example:
      admin_account_id: ID OF THE ADMIN ACCOUNT
      depends_on: 
        - ${aws_macie2_account.example}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `admin_account_id` - (Required) The AWS account ID for the account to designate as the delegated Amazon Macie administrator account for the organization.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The unique identifier (ID) of the macie organization admin account.

## Import

```bash
ytofu import aws_macie2_organization_admin_account.example abcd1
```
