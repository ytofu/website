# Appfabric App Authorization

Manage Appfabric App Authorization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appfabric_app_authorization:
    example:
      app: TERRAFORMCLOUD
      app_bundle_arn: ${aws_appfabric_app_bundle.arn}
      auth_type: apiKey
      credential:
        api_key_credential:
          api_key: exampleapikeytoken
      tenant:
        tenant_display_name: example
        tenant_identifier: example
```
