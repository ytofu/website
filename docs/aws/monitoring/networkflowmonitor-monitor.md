# Networkflowmonitor Monitor

Manage Networkflowmonitor Monitor resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      tags:
        Name: example

resource:
  aws_networkflowmonitor_monitor:
    example:
      monitor_name: example-monitor
      scope_arn: ${aws_networkflowmonitor_scope.example.scope_arn}
      local_resource:
        type: "AWS::EC2::VPC"
        identifier: ${aws_vpc.example.arn}
      remote_resource:
        type: "AWS::EC2::VPC"
        identifier: ${aws_vpc.example.arn}
      tags:
        Name: example
```
