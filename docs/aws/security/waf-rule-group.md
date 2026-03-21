# WAF Rule Group

Manage WAF Rule Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_rule:
    example:
      name: example
      metric_name: example

resource:
  aws_waf_rule_group:
    example:
      name: example
      metric_name: example
      activated_rule:
        action:
          type: COUNT
        priority: 50
        rule_id: ${aws_waf_rule.example.id}
```
