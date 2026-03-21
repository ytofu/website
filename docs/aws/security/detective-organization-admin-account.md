# Detective Organization Admin Account

Manage Detective Organization Admin Account resources using ytofu YAML.

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
