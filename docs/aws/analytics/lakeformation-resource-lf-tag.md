# Lakeformation Resource Lf Tag

Manage Lakeformation Resource Lf Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lakeformation_resource_lf_tag:
    example:
      database:
        name: ${aws_glue_catalog_database.example.name}
      lf_tag:
        key: ${aws_lakeformation_lf_tag.example.key}
        value: stowe
```
