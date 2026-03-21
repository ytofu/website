# Vpclattice Service Network VPC Association

Manage Vpclattice Service Network VPC Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_service_network_vpc_association:
    example:
      vpc_identifier: ${aws_vpc.example.id}
      service_network_identifier: ${aws_vpclattice_service_network.example.id}
      security_group_ids: 
        - ${aws_security_group.example.id}
```
