# Networkmanager Link Association

Manage Networkmanager Link Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_link_association:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      link_id: ${aws_networkmanager_link.example.id}
      device_id: ${aws_networkmanager_device.example.id}
```
