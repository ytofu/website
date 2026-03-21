# Datazone Asset Type

Manage Datazone Asset Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datazone_asset_type:
    test:
      description: example
      domain_identifier: ${aws_datazone_domain.test.id}
      name: example
      owning_project_identifier: ${aws_datazone_project.test.id}
```
