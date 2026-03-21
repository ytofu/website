# Autoscaling Attachment

Manage Autoscaling Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_autoscaling_attachment:
    example:
      autoscaling_group_name: ${aws_autoscaling_group.example.id}
      elb: ${aws_elb.example.id}
```
