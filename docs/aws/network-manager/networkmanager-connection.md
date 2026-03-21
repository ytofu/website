# Networkmanager Connection

Manage Networkmanager Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_connection:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      device_id: ${aws_networkmanager_device.example1.id}
      connected_device_id: ${aws_networkmanager_device.example2.id}
```
