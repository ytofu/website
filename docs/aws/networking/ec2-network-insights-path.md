# EC2 Network Insights Path

Manage EC2 Network Insights Path resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_network_insights_path:
    test:
      source: ${aws_network_interface.source.id}
      destination: ${aws_network_interface.destination.id}
      protocol: tcp
```
