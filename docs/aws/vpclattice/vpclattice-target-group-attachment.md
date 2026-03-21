# Vpclattice Target Group Attachment

Manage Vpclattice Target Group Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_target_group_attachment:
    example:
      target_group_identifier: ${aws_vpclattice_target_group.example.id}
      target:
        id: ${aws_lb.example.arn}
        port: 80
```
