# VPC Lattice Service Network

Create service networks using ytofu YAML.

## Basic Service Network

```yaml
resource:
  aws_vpclattice_service_network:
    example:
      name: example
      auth_type: NONE
```

## VPC Association

```yaml
resource:
  aws_vpclattice_service_network_vpc_association:
    example:
      vpc_identifier: ${aws_vpc.example.id}
      service_network_identifier: ${aws_vpclattice_service_network.example.id}
      security_group_ids:
        - ${aws_security_group.example.id}
```
