# Appfabric App Bundle

Manage Appfabric App Bundle resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appfabric_app_bundle:
    example:
      customer_managed_key_arn: ${awms_kms_key.example.arn}
      tags:
        Environment: test
```
