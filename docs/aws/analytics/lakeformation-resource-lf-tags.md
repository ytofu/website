# Lakeformation Resource Lf Tags

Manage Lakeformation Resource Lf Tags resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lakeformation_lf_tag:
    example:
      key: right
      values: 
        - abbey
        - village
        - luffield
        - woodcote
        - copse
        - chapel
        - stowe
        - club

resource:
  aws_lakeformation_resource_lf_tags:
    example:
      database:
        name: ${aws_glue_catalog_database.example.name}
      lf_tag:
        key: ${aws_lakeformation_lf_tag.example.key}
        value: stowe
```

## Multiple Tags Example

```yaml
resource:
  aws_lakeformation_lf_tag:
    example:
      key: right
      values: 
        - abbey
        - village
        - luffield
        - woodcote
        - copse
        - chapel
        - stowe
        - club

resource:
  aws_lakeformation_lf_tag:
    example2:
      key: left
      values: 
        - farm
        - theloop
        - aintree
        - brooklands
        - maggotts
        - becketts
        - vale

resource:
  aws_lakeformation_resource_lf_tags:
    example:
      database:
        name: ${aws_glue_catalog_database.example.name}
      lf_tag:
        key: right
        value: luffield
      lf_tag:
        key: left
        value: aintree
```
