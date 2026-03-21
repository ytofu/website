# Networkfirewall VPC Endpoint Association

Manage Networkfirewall VPC Endpoint Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_vpc_endpoint_association:
    example:
      firewall_arn: ${aws_networkfirewall_firewall.example.arn}
      vpc_id: ${aws_vpc.example.id}
      subnet_mapping:
        subnet_id: ${aws_subnet.example.id}
      tags:
        Name: example endpoint
```
