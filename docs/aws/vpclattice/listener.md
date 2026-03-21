# VPC Lattice Listener

Create listeners for VPC Lattice services using ytofu YAML.

## HTTP Listener

```yaml
resource:
  aws_vpclattice_listener:
    example:
      name: example
      protocol: HTTP
      service_identifier: ${aws_vpclattice_service.example.id}
      default_action:
        forward:
          - target_groups:
              - target_group_identifier: ${aws_vpclattice_target_group.example.id}
                weight: 100
```

## HTTPS Listener

```yaml
resource:
  aws_vpclattice_listener:
    example:
      name: example
      protocol: HTTPS
      port: 443
      service_identifier: ${aws_vpclattice_service.example.id}
      default_action:
        forward:
          - target_groups:
              - target_group_identifier: ${aws_vpclattice_target_group.example.id}
```
