# Securityhub Organization Configuration

Manage Securityhub Organization Configuration resources using ytofu YAML.

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
