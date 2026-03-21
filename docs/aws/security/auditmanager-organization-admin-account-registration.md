# Resource: aws_auditmanager_organization_admin_account_registration

ytofu resource for managing AWS Audit Manager Organization Admin Account Registration.

## Basic Example

```yaml
resource:
  aws_auditmanager_organization_admin_account_registration:
    example:
      admin_account_id: 123456789012
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `admin_account_id` - (Required) Identifier for the organization administrator account.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier for the organization administrator account.
* `organization_id` - Identifier for the organization.

## Import

```bash
ytofu import aws_auditmanager_organization_admin_account_registration.example 123456789012
```
