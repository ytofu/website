# Securityhub Organization Admin Account

Manage Securityhub Organization Admin Account resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - securityhub.amazonaws.com
      feature_set: ALL

resource:
  aws_securityhub_account:
    example:

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
