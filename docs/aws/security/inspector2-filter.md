# Inspector2 Filter

Manage Inspector2 Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_inspector2_filter:
    example:
      name: test
      action: NONE
      filter_criteria:
        aws_account_id:
          comparison: EQUALS
          value: 111222333444
```
