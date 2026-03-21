# Codecommit Approval Rule Template Association

Manage Codecommit Approval Rule Template Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codecommit_approval_rule_template_association:
    example:
      approval_rule_template_name: ${aws_codecommit_approval_rule_template.example.name}
      repository_name: ${aws_codecommit_repository.example.repository_name}
```
