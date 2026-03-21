# Networkmanager Site

Manage Networkmanager Site resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_global_network:
    example:

resource:
  aws_networkmanager_site:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
```
