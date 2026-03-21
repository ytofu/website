# Licensemanager License Configuration

Manage Licensemanager License Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_licensemanager_license_configuration:
    example:
      name: Example
      description: Example
      license_count: 10
      license_count_hard_limit: true
      license_counting_type: Socket
      license_rules:
        - "#minimumSockets=2"
      tags:
        foo: barr
```
