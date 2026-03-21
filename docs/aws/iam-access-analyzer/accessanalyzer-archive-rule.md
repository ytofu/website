# Accessanalyzer Archive Rule

Manage Accessanalyzer Archive Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_accessanalyzer_archive_rule:
    example:
      analyzer_name: example-analyzer
      rule_name: example-rule
      filter:
        criteria: "condition.aws:UserId"
        eq: 
          - userid
      filter:
        criteria: error
        exists: true
      filter:
        criteria: isPublic
        eq: 
          - false
```
