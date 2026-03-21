# IAM Organizations Features

Manage IAM Organizations Features resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - iam.amazonaws.com
      feature_set: ALL

resource:
  aws_iam_organizations_features:
    example:
      enabled_features:
        - RootCredentialsManagement
        - RootSessions
```
