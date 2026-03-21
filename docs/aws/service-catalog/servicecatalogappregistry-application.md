# Servicecatalogappregistry Application

Manage Servicecatalogappregistry Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app
```

## Connecting Resources

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app

resource:
  aws_s3_bucket:
    bucket:
      bucket: example-bucket
      tags: ${aws_servicecatalogappregistry_application.example.application_tag}
```
