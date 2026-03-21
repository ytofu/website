# Quicksight Template Alias

Manage Quicksight Template Alias resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_template_alias:
    example:
      alias_name: example-alias
      template_id: ${aws_quicksight_template.test.template_id}
      template_version_number: ${aws_quicksight_template.test.version_number}
```
