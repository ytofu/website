# IOT Topic Rule Destination

Manage IOT Topic Rule Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_topic_rule_destination:
    example:
      vpc_configuration:
        role_arn: ${aws_iam_role.example.arn}
        security_groups: 
          - ${aws_security_group.example.id}
        subnet_ids: ${aws_subnet.example[*].id}
        vpc_id: ${aws_vpc.example.id}
```
