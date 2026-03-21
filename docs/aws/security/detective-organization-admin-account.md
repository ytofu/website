# Resource: aws_detective_organization_admin_account

Manages a Detective Organization Admin Account. The AWS account utilizing this resource must be an Organizations primary account. More information about Organizations support in Detective can be found in the [Detective User Guide](https://docs.aws.amazon.com/detective/latest/adminguide/accounts-orgs-transition.html).

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - detective.amazonaws.com
      feature_set: ALL

resource:
  aws_detective_organization_admin_account:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      account_id: 123456789012
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Required) AWS account identifier to designate as a delegated administrator for Detective.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS account identifier.

## Import

```bash
ytofu import aws_detective_organization_admin_account.example 123456789012
```
