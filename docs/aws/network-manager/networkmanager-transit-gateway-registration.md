# Networkmanager Transit Gateway Registration

Manage Networkmanager Transit Gateway Registration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_global_network:
    example:
      description: example

resource:
  aws_ec2_transit_gateway:
    example:

resource:
  aws_networkmanager_transit_gateway_registration:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      transit_gateway_arn: ${aws_ec2_transit_gateway.example.arn}
```
