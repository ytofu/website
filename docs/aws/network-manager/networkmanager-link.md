# Networkmanager Link

Manage Networkmanager Link resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_link:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      site_id: ${aws_networkmanager_site.example.id}
      bandwidth:
        upload_speed: 10
        download_speed: 50
      provider_name: MegaCorp
```
