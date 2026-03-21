# Config Organization Managed Rule

Manage Config Organization Managed Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - config-multiaccountsetup.amazonaws.com
      feature_set: ALL

resource:
  aws_config_organization_managed_rule:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      name: example
      rule_identifier: IAM_PASSWORD_POLICY
```
