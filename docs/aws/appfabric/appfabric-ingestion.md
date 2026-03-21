# Appfabric Ingestion

Manage Appfabric Ingestion resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appfabric_ingestion:
    example:
      app: OKTA
      app_bundle_arn: ${aws_appfabric_app_bundle.example.arn}
      tenant_id: example.okta.com
      ingestion_type: auditLog
      tags:
        Environment: test
```
