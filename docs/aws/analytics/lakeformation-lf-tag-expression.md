# Lakeformation Lf Tag Expression

Manage Lakeformation Lf Tag Expression resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lakeformation_lf_tag:
    example:
      key: example
      values: 
        - value

resource:
  aws_lakeformation_lf_tag_expression:
    example:
      name: example
      expression:
        tag_key: ${aws_lakeformation_lf_tag.example.key}
        tag_values: ${aws_lakeformation_lf_tag.example.values}
```
