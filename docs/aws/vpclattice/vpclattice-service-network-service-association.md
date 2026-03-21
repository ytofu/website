# Vpclattice Service Network Service Association

Manage Vpclattice Service Network Service Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_service_network_service_association:
    example:
      service_identifier: ${aws_vpclattice_service.example.id}
      service_network_identifier: ${aws_vpclattice_service_network.example.id}
```
