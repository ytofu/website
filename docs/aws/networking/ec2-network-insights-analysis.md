# EC2 Network Insights Analysis

Manage EC2 Network Insights Analysis resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_network_insights_path:
    path:
      source: ${aws_network_interface.source.id}
      destination: ${aws_network_interface.destination.id}
      protocol: tcp

resource:
  aws_ec2_network_insights_analysis:
    analysis:
      network_insights_path_id: ${aws_ec2_network_insights_path.path.id}
```
