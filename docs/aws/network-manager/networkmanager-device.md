# Networkmanager Device

Manage Networkmanager Device resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_device:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      site_id: ${aws_networkmanager_site.example.id}
```
