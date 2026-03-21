# Vpclattice Service Network Resource Association

Manage Vpclattice Service Network Resource Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_service_network_resource_association:
    example:
      resource_configuration_identifier: ${aws_vpclattice_resource_configuration.example.id}
      service_network_identifier: ${aws_vpclattice_service_network.example.id}
      tags:
        Name: Example
```
