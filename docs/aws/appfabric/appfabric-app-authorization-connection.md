# Appfabric App Authorization Connection

Manage Appfabric App Authorization Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appfabric_app_authorization_connection:
    example:
      app_authorization_arn: ${aws_appfabric_app_authorization.test.arn}
      app_bundle_arn: ${aws_appfabric_app_bundle.arn}
```
