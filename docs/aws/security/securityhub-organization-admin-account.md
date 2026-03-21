# Resource: aws_securityhub_organization_admin_account

Manages a Security Hub administrator account for an organization. The AWS account utilizing this resource must be an Organizations primary account. More information about Organizations support in Security Hub can be found in the [Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/designate-orgs-admin-account.html).

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - securityhub.amazonaws.com
      feature_set: ALL

  aws_securityhub_account:
    example:

  aws_securityhub_organization_admin_account:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      admin_account_id: 123456789012

  aws_securityhub_organization_configuration:
    example:
      auto_enable: true```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `admin_account_id` - (Required) The AWS account identifier of the account to designate as the Security Hub administrator account.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS account identifier.

## Import

```bash
ytofu import aws_securityhub_organization_admin_account.example 123456789012
```
