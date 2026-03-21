# VPC Lattice Listener Rule

Create routing rules for VPC Lattice listeners using ytofu YAML.

## Path-Based Routing

```yaml
resource:
  aws_vpclattice_listener_rule:
    example:
      name: example
      listener_identifier: ${aws_vpclattice_listener.example.listener_id}
      service_identifier: ${aws_vpclattice_service.example.id}
      priority: 10
      match:
        http_match:
          path_match:
            match:
              prefix: /api
      action:
        forward:
          target_groups:
            - target_group_identifier: ${aws_vpclattice_target_group.api.id}
              weight: 100
```
