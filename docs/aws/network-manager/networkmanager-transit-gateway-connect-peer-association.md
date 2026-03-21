# Networkmanager Transit Gateway Connect Peer Association

Manage Networkmanager Transit Gateway Connect Peer Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_transit_gateway_connect_peer_association:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      device_id: ${aws_networkmanager_device.example.id}
      transit_gateway_connect_peer_arn: ${aws_ec2_transit_gateway_connect_peer.example.arn}
```
