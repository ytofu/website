# Resource: aws_guardduty_organization_admin_account

Manages a GuardDuty Organization Admin Account. The AWS account utilizing this resource must be an Organizations primary account. More information about Organizations support in GuardDuty can be found in the [GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_organizations.html).

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - guardduty.amazonaws.com
      feature_set: ALL

  aws_guardduty_detector:
    example:

  aws_guardduty_organization_admin_account:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      admin_account_id: 123456789012```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `admin_account_id` - (Required) AWS account identifier to designate as a delegated administrator for GuardDuty.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_guardduty_organization_admin_account.example 123456789012
```
