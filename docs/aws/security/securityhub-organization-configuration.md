# Resource: aws_securityhub_organization_configuration

Manages the Security Hub Organization Configuration.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - securityhub.amazonaws.com
      feature_set: ALL

resource:
  aws_securityhub_organization_admin_account:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      admin_account_id: 123456789012

resource:
  aws_securityhub_organization_configuration:
    example:
      auto_enable: true
```

## Central Configuration

```yaml
resource:
  aws_securityhub_organization_admin_account:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      admin_account_id: 123456789012

resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: ALL_REGIONS
      depends_on: 
        - ${aws_securityhub_organization_admin_account.example}

resource:
  aws_securityhub_organization_configuration:
    example:
      auto_enable: false
      auto_enable_standards: NONE
      organization_configuration:
        configuration_type: CENTRAL
      depends_on: 
        - ${aws_securityhub_finding_aggregator.example}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `auto_enable` - (Required) Whether to automatically enable Security Hub for new accounts in the organization.
* `auto_enable_standards` - (Optional) Whether to automatically enable Security Hub default standards for new member accounts in the organization. By default, this parameter is equal to `DEFAULT`, and new member accounts are automatically enabled with default Security Hub standards. To opt out of enabling default standards for new member accounts, set this parameter equal to `NONE`.
* `organization_configuration` - (Optional) Provides information about the way an organization is configured in Security Hub.

`organization_configuration` supports the following:

* `configuration_type` - (Required) Indicates whether the organization uses local or central configuration. If using central configuration, `auto_enable` must be set to `false` and `auto_enable_standards` set to `NONE`. More information can be found in the [documentation for central configuration](https://docs.aws.amazon.com/securityhub/latest/userguide/central-configuration-intro.html). Valid values: `LOCAL`, `CENTRAL`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Account ID.

## Timeouts

Configuration options:

* `create` - (Default `180s`)
* `update` - (Default `180s`)
* `delete` - (Default `180s`)

## Import

```bash
ytofu import aws_securityhub_organization_configuration.example 123456789012
```
