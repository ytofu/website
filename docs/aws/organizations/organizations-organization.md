# Organizations Organization

Manage Organizations Organization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    org:
      aws_service_access_principals:
        - cloudtrail.amazonaws.com
        - config.amazonaws.com
      feature_set: ALL
```
