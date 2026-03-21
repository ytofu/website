# Resourcegroups Resource

Manage Resourcegroups Resource resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_host:
    example:
      instance_family: t3
      availability_zone: us-east-1a
      host_recovery: off
      auto_placement: on

resource:
  aws_resourcegroups_group:
    example:
      name: example

resource:
  aws_resourcegroups_resource:
    example:
      group_arn: ${aws_resourcegroups_group.example.arn}
      resource_arn: ${aws_ec2_host.example.arn}
```
