# Directory Service Radius Settings

Manage Directory Service Radius Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_directory_service_radius_settings:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      authentication_protocol: PAP
      display_label: example
      radius_port: 1812
      radius_retries: 4
      radius_servers: 
        - 10.0.1.5
      radius_timeout: 1
      shared_secret: 12345678
```
