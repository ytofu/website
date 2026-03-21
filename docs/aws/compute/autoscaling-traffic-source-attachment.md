# Autoscaling Traffic Source Attachment

Manage Autoscaling Traffic Source Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_autoscaling_traffic_source_attachment:
    example:
      autoscaling_group_name: ${aws_autoscaling_group.example.id}
      traffic_source:
        identifier: ${aws_lb_target_group.example.arn}
        type: elbv2
```
