# WAF Size Constraint Set

Manage WAF Size Constraint Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_size_constraint_set:
    size_constraint_set:
      name: tfsize_constraints
      size_constraints:
        text_transformation: NONE
        comparison_operator: EQ
        size: 4096
        field_to_match:
          type: BODY
```
